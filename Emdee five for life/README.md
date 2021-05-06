# Emdee five for life #
1. I've installed the "Scripty" plugin (https://chrome.google.com/webstore/detail/scripty-javascript-inject/milkbiaeapddfnpenedfgbfdacpbcbam/related)
So I will be able to inject my script on page load
2. I wrote a script that takes the random string from the header, hashing it, and submitting
```javascript
let text = document.getElementsByTagName("h3")[0].textContent;
let input = document.getElementsByTagName("input")[0];
let submit = document.getElementsByTagName("input")[1];

if (!document.body.innerText.includes("HTB{")) {
	input.value = md5(text);
	submit.click();
}

function md5(r) {
	var n = "0123456789abcdef";

	function t(r) {
		var t, u = "";
		for (t = 0; t <= 3; t++) u += n.charAt(r >> 8 * t + 4 & 15) + n.charAt(r >> 8 * t & 15);
		return u
	}

	function u(r, n) {
		var t = (65535 & r) + (65535 & n);
		return (r >> 16) + (n >> 16) + (t >> 16) << 16 | 65535 & t
	}

	function e(r, n, t, e, f, o) {
		return u((c = u(u(n, r), u(e, o))) << (a = f) | c >>> 32 - a, t);
		var c, a
	}

	function f(r, n, t, u, f, o, c) {
		return e(n & t | ~n & u, r, n, f, o, c)
	}

	function o(r, n, t, u, f, o, c) {
		return e(n & u | t & ~u, r, n, f, o, c)
	}

	function c(r, n, t, u, f, o, c) {
		return e(n ^ t ^ u, r, n, f, o, c)
	}

	function a(r, n, t, u, f, o, c) {
		return e(t ^ (n | ~u), r, n, f, o, c)
	}
	var i, h, v, g, l, A = function(r) {
			var n, t = 1 + (r.length + 8 >> 6),
				u = new Array(16 * t);
			for (n = 0; n < 16 * t; n++) u[n] = 0;
			for (n = 0; n < r.length; n++) u[n >> 2] |= r.charCodeAt(n) << n % 4 * 8;
			return u[n >> 2] |= 128 << n % 4 * 8, u[16 * t - 2] = 8 * r.length, u
		}(r),
		d = 1732584193,
		b = -271733879,
		m = -1732584194,
		w = 271733878;
	for (i = 0; i < A.length; i += 16) h = d, v = b, g = m, l = w, d = f(d, b, m, w, A[i + 0], 7, -680876936), w = f(w, d, b, m, A[i + 1], 12, -389564586), m = f(m, w, d, b, A[i + 2], 17, 606105819), b = f(b, m, w, d, A[i + 3], 22, -1044525330), d = f(d, b, m, w, A[i + 4], 7, -176418897), w = f(w, d, b, m, A[i + 5], 12, 1200080426), m = f(m, w, d, b, A[i + 6], 17, -1473231341), b = f(b, m, w, d, A[i + 7], 22, -45705983), d = f(d, b, m, w, A[i + 8], 7, 1770035416), w = f(w, d, b, m, A[i + 9], 12, -1958414417), m = f(m, w, d, b, A[i + 10], 17, -42063), b = f(b, m, w, d, A[i + 11], 22, -1990404162), d = f(d, b, m, w, A[i + 12], 7, 1804603682), w = f(w, d, b, m, A[i + 13], 12, -40341101), m = f(m, w, d, b, A[i + 14], 17, -1502002290), d = o(d, b = f(b, m, w, d, A[i + 15], 22, 1236535329), m, w, A[i + 1], 5, -165796510), w = o(w, d, b, m, A[i + 6], 9, -1069501632), m = o(m, w, d, b, A[i + 11], 14, 643717713), b = o(b, m, w, d, A[i + 0], 20, -373897302), d = o(d, b, m, w, A[i + 5], 5, -701558691), w = o(w, d, b, m, A[i + 10], 9, 38016083), m = o(m, w, d, b, A[i + 15], 14, -660478335), b = o(b, m, w, d, A[i + 4], 20, -405537848), d = o(d, b, m, w, A[i + 9], 5, 568446438), w = o(w, d, b, m, A[i + 14], 9, -1019803690), m = o(m, w, d, b, A[i + 3], 14, -187363961), b = o(b, m, w, d, A[i + 8], 20, 1163531501), d = o(d, b, m, w, A[i + 13], 5, -1444681467), w = o(w, d, b, m, A[i + 2], 9, -51403784), m = o(m, w, d, b, A[i + 7], 14, 1735328473), d = c(d, b = o(b, m, w, d, A[i + 12], 20, -1926607734), m, w, A[i + 5], 4, -378558), w = c(w, d, b, m, A[i + 8], 11, -2022574463), m = c(m, w, d, b, A[i + 11], 16, 1839030562), b = c(b, m, w, d, A[i + 14], 23, -35309556), d = c(d, b, m, w, A[i + 1], 4, -1530992060), w = c(w, d, b, m, A[i + 4], 11, 1272893353), m = c(m, w, d, b, A[i + 7], 16, -155497632), b = c(b, m, w, d, A[i + 10], 23, -1094730640), d = c(d, b, m, w, A[i + 13], 4, 681279174), w = c(w, d, b, m, A[i + 0], 11, -358537222), m = c(m, w, d, b, A[i + 3], 16, -722521979), b = c(b, m, w, d, A[i + 6], 23, 76029189), d = c(d, b, m, w, A[i + 9], 4, -640364487), w = c(w, d, b, m, A[i + 12], 11, -421815835), m = c(m, w, d, b, A[i + 15], 16, 530742520), d = a(d, b = c(b, m, w, d, A[i + 2], 23, -995338651), m, w, A[i + 0], 6, -198630844), w = a(w, d, b, m, A[i + 7], 10, 1126891415), m = a(m, w, d, b, A[i + 14], 15, -1416354905), b = a(b, m, w, d, A[i + 5], 21, -57434055), d = a(d, b, m, w, A[i + 12], 6, 1700485571), w = a(w, d, b, m, A[i + 3], 10, -1894986606), m = a(m, w, d, b, A[i + 10], 15, -1051523), b = a(b, m, w, d, A[i + 1], 21, -2054922799), d = a(d, b, m, w, A[i + 8], 6, 1873313359), w = a(w, d, b, m, A[i + 15], 10, -30611744), m = a(m, w, d, b, A[i + 6], 15, -1560198380), b = a(b, m, w, d, A[i + 13], 21, 1309151649), d = a(d, b, m, w, A[i + 4], 6, -145523070), w = a(w, d, b, m, A[i + 11], 10, -1120210379), m = a(m, w, d, b, A[i + 2], 15, 718787259), b = a(b, m, w, d, A[i + 9], 21, -343485551), d = u(d, h), b = u(b, v), m = u(m, g), w = u(w, l);
	return t(d) + t(b) + t(m) + t(w)
}
```
3. Refresh the page, and that's it.
