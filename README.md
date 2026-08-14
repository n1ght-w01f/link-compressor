# ⚡ Link Compressor (GitHub Pages Edition)

> ⚠️ **Note / PoC:** This version is a **Proof of Concept (PoC)** adapted to run and deploy **100% statically on GitHub Pages** without requiring custom short domains or backend infrastructure. 
> 
> Due to how subdomains work on GitHub Pages (`your-username.github.io/repository-name`), **it is impossible to shorten the final length of links**. The sole purpose of this fork is to demonstrate the technical operation of the URL compression and encoding algorithm hosted on a free static platform.

---

## 📌 Original Project & Credits

All technical credit, algorithm design, and original code belong to **PortalRunner**.

* 🌐 **Official Website:** [ha.mr](https://ha.mr) *(Use the official website to actually compress links!)*
* 🐙 **Official Repository:** [p2r3/ha.mr](https://github.com/p2r3/ha.mr)
* 📺 **Explainer Video:** To deep dive into the information theory, Huffman coding, and mechanics behind this project, watch the original video on YouTube: [I Made the World's First "Link Compressor"](https://www.youtube.com/watch?v=TOr1Vvji6jA) by **PortalRunner**.

---

## 🛠️ Changes in this Fork

1. **Dynamic Routing for GitHub Pages:** Adapted generated URLs using `window.location` so it works out-of-the-box with the username and repository name of anyone who forks this project.
2. **Redirect Support:** Adjusted client-side logic to properly handle hash (`#`) decoding and QR code redirection parameters without requiring a 4-character domain.

---

# ha.mr
Compresses links and optimizes QR codes entirely in the browser, without a back-end database.

## How
1. Common parts of the link (e.g. protocol, `www.` prefix, `index.html`) are manually detected and reduced to individual bits. If present, the port is encoded as a raw numeric value.
2. Second-level and top-level domains are matched against a Huffman-coded dictionary of the most common websites and TLDs.
3. The rest of the link is split into parts, and each segment is either fitted to a predefined character set, or Huffman coded.
4. For links, the output is encoded in the full character set of a URL. (I've been informed that square brackets `[]` are not supposed to be a part of this set, but it's too late to change that now.)
5. For QR codes, the output uses the alphanumeric character set to remove overhead compared to other QR code generators.

## Acknowledgements
- https://www.npmjs.com/package/qrcode
- https://github.com/smythp/reddit_links_dataset
- https://github.com/ada-url/url-dataset
