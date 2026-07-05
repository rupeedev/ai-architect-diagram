---
description: Generate on-prem OpenShift/OCP + CNCF architecture diagrams as draw.io (.drawio) files using embedded-SVG icons that render reliably
---

# OpenShift / On-Prem Architecture Diagram Generator (draw.io)

Generate professional **on-prem OpenShift / Kubernetes** architecture diagrams as native **draw.io** (`.drawio`) files. Use for OCP, bare-metal/VM Kubernetes, CNCF-stack, and data-centre topologies.

**This is the on-prem counterpart to `/design-aws-diagram`.** Do NOT use AWS icons (EC2, VPC, S3, Lambda) for on-prem OpenShift — they misrepresent the architecture and a technical audience will reject it. Use OpenShift/Kubernetes/CNCF iconography instead.

## Input
$ARGUMENTS

## Why embedded SVG (verified, not optional)

draw.io's built-in stencil libraries do **not** render reliably at CLI/PNG export:
- `shape=mxgraph.cloud_native.*` and `shape=mxgraph.networking.*` → **silently fall back to empty boxes on export** (this is the #1 cause of "barebone" diagrams).
- `shape=mxgraph.kubernetes.pod` *does* render, but coverage is incomplete and there are **no vendor-neutral Redis/Kafka/Istio/Prometheus icons** — only cloud-vendor-flavoured ones (AWS/GCP/Azure), which reintroduce the wrong-cloud problem.

**Solution: embed each icon as an inline SVG `data:` URI** on a `shape=image` cell. These render identically in draw.io desktop **and** headless export, with full control and correct on-prem/CNCF iconography.

## THREE GOTCHAS THAT WILL SILENTLY BLANK THE WHOLE FILE

1. **URL-encode the SVG.** The `image=` value must be `data:image/svg+xml,` + `urllib.parse.quote(svg)`. Raw `<`, `>`, `"`, `#`, `&` in the data URI break the style attribute. `quote()` (default `safe='/'`) encodes all of them — good.
2. **XML-escape every `value=` attribute.** If you build `.drawio` XML as raw strings, literal `<b>`, `<br>`, or `&` inside `value="..."` is **invalid XML → draw.io fails to parse the entire file → blank render.** Escape `& < > "` (or build with `xml.etree.ElementTree`, which auto-escapes). Styles are safe (the encoded data URI has no raw `<`/`>`/`&`/`"`).
3. **`--page-index` is unreliable across builds.** In testing it behaved 1-based (index `2` = the 2nd content page). Always **render and visually confirm** you exported the page you meant.

## Export / render workflow (macOS draw.io desktop)

```bash
"/Applications/draw.io.app/Contents/MacOS/draw.io" \
  --export --page-index N --output out.png --width 1750 --border 12 file.drawio
```
Then Read the PNG to verify. `timeout` is unavailable on macOS — the app exits on its own. Iterate: build → export → Read → fix.

## Icon library (original simplified brand-coloured marks — no copied logos)

Store as a dict, encode with `img(k)`. Verified-rendering set:

```python
import urllib.parse
SVG = {
 "pod":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><circle cx="24" cy="24" r="22" fill="#326CE5"/><path d="M24 9l11 6v14l-11 6-11-6V15z" fill="none" stroke="white" stroke-width="2.4"/><circle cx="24" cy="24" r="4" fill="white"/></svg>',
 "ocp":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><circle cx="24" cy="24" r="21" fill="#EE0000"/><path d="M24 11l11 6.5v13L24 37l-11-6.5v-13z" fill="none" stroke="white" stroke-width="2.6"/><circle cx="24" cy="24" r="3.5" fill="white"/></svg>',
 "route":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="#EE0000"/><circle cx="14" cy="24" r="4" fill="white"/><circle cx="34" cy="14" r="4" fill="white"/><circle cx="34" cy="34" r="4" fill="white"/><path d="M17 24h9M26 24l6-9M26 24l6 9" stroke="white" stroke-width="2.4" fill="none"/></svg>',
 "istio":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="#466BB0"/><path d="M31 8L17 40h14z" fill="white"/><path d="M31 8L17 40l14-4z" fill="#AEC4E8"/></svg>',
 "prometheus":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="#E6522C"/><path d="M24 8c5 6 2 10 0 12-3-2-4-7 0-12z" fill="white"/><path d="M13 29a11 8 0 0022 0z" fill="white"/><rect x="16" y="30" width="16" height="3" fill="#E6522C"/></svg>',
 "redis":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="white" stroke="#D82C20" stroke-width="2"/><path d="M24 11l15 6-15 6-15-6z" fill="#D82C20"/><path d="M9 24l15 6 15-6M9 30l15 6 15-6" fill="none" stroke="#D82C20" stroke-width="2.4"/></svg>',
 "kafka":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="white" stroke="#231F20" stroke-width="2"/><circle cx="16" cy="15" r="4" fill="#231F20"/><circle cx="16" cy="33" r="4" fill="#231F20"/><circle cx="33" cy="24" r="5" fill="#231F20"/><path d="M19 16l10 6M19 32l10-6" stroke="#231F20" stroke-width="2.4"/></svg>',
 "cdc":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="#4D9221"/><path d="M8 18h22M8 30h22" stroke="white" stroke-width="3"/><path d="M26 12l9 6-9 6M26 24l9 6-9 6" fill="white"/></svg>',
 "git":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect width="48" height="48" rx="8" fill="#F05133"/><circle cx="15" cy="15" r="4" fill="white"/><circle cx="15" cy="34" r="4" fill="white"/><circle cx="33" cy="24" r="4" fill="white"/><path d="M15 19v11M15 29c0-6 18-1 18-5" stroke="white" stroke-width="2.6" fill="none"/></svg>',
 "waf":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><path d="M24 5l17 5v11c0 12-9 19-17 22-8-3-17-10-17-22V10z" fill="#1F4E8C"/><path d="M15 24l6 6 12-13" stroke="white" stroke-width="3.2" fill="none"/></svg>',
 "gslb":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><circle cx="24" cy="24" r="21" fill="#002060"/><ellipse cx="24" cy="24" rx="21" ry="8.5" fill="none" stroke="white" stroke-width="1.4"/><ellipse cx="24" cy="24" rx="8.5" ry="21" fill="none" stroke="white" stroke-width="1.4"/><path d="M3 24h42" stroke="white" stroke-width="1.4"/><circle cx="24" cy="24" r="3.5" fill="white"/></svg>',
 "web":'<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 48 48"><rect x="7" y="9" width="34" height="9" rx="2" fill="#5A6B7B"/><rect x="7" y="20" width="34" height="9" rx="2" fill="#5A6B7B"/><rect x="7" y="31" width="34" height="9" rx="2" fill="#5A6B7B"/><circle cx="13" cy="13.5" r="2" fill="#37D67A"/><circle cx="13" cy="24.5" r="2" fill="#37D67A"/><circle cx="13" cy="35.5" r="2" fill="#37D67A"/></svg>',
}
def img(k): return "data:image/svg+xml,"+urllib.parse.quote(SVG[k])
```
Brand colours: k8s `#326CE5`, OpenShift/Red Hat `#EE0000`, Istio `#466BB0`, Prometheus `#E6522C`, Redis `#D82C20`, Kafka `#231F20`, Git `#F05133`. Add new tools the same way (simplified geometric mark + brand colour; do not paste copyrighted logo files).

## Builder pattern

```python
def esc(s): return s.replace('&','&amp;').replace('<','&lt;').replace('>','&gt;').replace('"','&quot;')
cells=['<mxCell id="0"/><mxCell id="1" parent="0"/>']
def add(cid,val,style,x,y,w,h):
    cells.append(f'<mxCell id="{cid}" value="{esc(val)}" style="{style}" vertex="1" parent="1"><mxGeometry x="{x}" y="{y}" width="{w}" height="{h}" as="geometry"/></mxCell>')
def comp(cid,k,label,cx,y,s=46,lw=240):        # centred icon + label-below
    add(cid,'',f'shape=image;html=1;image={img(k)};',cx-s//2,y,s,s)
    if label: add(cid+'_l',label,'text;html=1;align=center;fontSize=10;fontStyle=1;fontColor=#333333;',cx-lw//2,y+s+1,lw,16)
def edge(cid,s,t):                              # clean vertical orthogonal
    cells.append(f'<mxCell id="{cid}" style="edgeStyle=orthogonalEdgeStyle;html=1;endArrow=block;strokeColor=#5A6B7B;strokeWidth=1.6;exitX=0.5;exitY=1;entryX=0.5;entryY=0;" edge="1" parent="1" source="{s}" target="{t}"><mxGeometry relative="1" as="geometry"/></mxCell>')
# multi-page: '<mxfile host="Electron">' + '<diagram id=".." name="..">...' *N + '</mxfile>'
```

## Design standards (what makes it tier-1)

- **Centre components on a vertical axis** so `orthogonalEdgeStyle` edges drop straight (misaligned icons → diagonal spaghetti).
- **Labels as separate centred text cells** below icons (image-cell labels overflow the icon width).
- **Zone containers** (data-centre / cluster) as titled rounded rects; draw component icons on top at absolute coords (simpler than real swimlane children).
- **Numbered callout markers**: red `#CC0000` for problems, green `#1F6F5C` for solutions, as `ellipse` cells with a white bold number; keep a matching legend panel.
- **Header bar** (dark), a "How to read" note, and a right-side **findings/legend panel**.
- **Current-state vs target**: red theme + real topology; green theme + target components (mesh, CDC, etc.). Keep marker numbers identical across both so they tell one story.
- Note in text when something isn't representable in the view (e.g. data-tier not in an app-topology diagram) rather than faking it.

## Steps
1. Parse the request; identify components, zones, and flow.
2. Assemble the icon set (reuse the library; add brand-coloured marks for new tools).
3. Build the `.drawio` with the pattern above (escape values, encode SVGs).
4. Export each page to PNG and **Read it to verify** — fix overlaps/blank renders; iterate.
5. Keep any source/reference page untouched; write new pages alongside and keep a `.bak`.
