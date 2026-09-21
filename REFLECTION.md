# Reflection

## 1. HTTP Request Path to GitHub Pages

Here is what happens behind the scenes when loading `https://nanzib.github.io`:

1. **DNS Lookup:** The browser checks if it already knows the IP address for `nanzib.github.io`. If it doesn't, it queries a DNS resolver to look up GitHub's nameservers and grab the edge server IP.
2. **Connection & Handshake:** The browser opens a TCP connection with GitHub's server, followed by a TLS handshake to handle HTTPS encryption.
3. **HTTP GET Request:** The browser sends a `GET /` request. It includes the `Host: nanzib.github.io` header so GitHub's servers know which repository's static files to pull from.
4. **Server Response:** GitHub finds `index.html` in the root folder and sends it back with a `200 OK` status.
5. **Fetching Assets:** As the browser reads through the HTML, it hits the links for `style.css` and `assets/profile.png`. It makes separate GET requests for those two files, applies the styles, and paints the page.

---

## 2. AI Attribution & Bug Fix

### Prompt Used
> "Show me a minimal example of an intentional 3-way CSS specificity conflict on an h1 element using element, class, and ID selectors where the ID rule wins."

### The Error
The generated snippet set up the conflict like this:

```css
h1 { color: gray; }
#site-header h1 { color: blue; }
#candidate-name { color: black; }
```

The issue was in `#site-header h1`. Because it paired an ID with an element selector, its specificity score came out to **(1, 0, 1)**. The rule that was supposed to win—`#candidate-name`—only had a score of **(1, 0, 0)**. 

Because of that extra element selector, the blue color overrode the black text, breaking the intended hierarchy and defeating the point of the challenge.

### The Fix
I swapped `#site-header` out for a class selector instead:

```css
h1 { color: #6b7280; }                 /* (0, 0, 1) */
.header-text h1 { color: #374151; }    /* (0, 1, 1) */
#candidate-name { color: #111827; }    /* (1, 0, 0) */
```

Changing it to `.header-text h1` dropped that rule to **(0, 1, 1)**, letting `#candidate-name` take priority with **(1, 0, 0)** as intended.