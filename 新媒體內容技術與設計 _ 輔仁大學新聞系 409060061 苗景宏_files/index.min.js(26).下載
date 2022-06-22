!function() {
    var sandbox;
    (sandbox = function(wopt) {
        var root, container;
        return this.opt = wopt = null == wopt ? {} : wopt, this.proxy = {}, this.root = root = wopt.root ? "string" == typeof wopt.root ? document.querySelector(wopt.root) : wopt.root : void 0, 
        this.container = container = (container = root && root.parentNode) ? container : this.opt.container ? "string" == typeof wopt.container ? document.querySelector(wopt.container) : wopt.container : void 0, 
        container = container || (this.container = null), this.container && (root || (this.root = root = document.createElement("iframe")), 
        this.root.parentNode || container.appendChild(root), root.setAttribute("sandbox", wopt.sandbox || "allow-scripts allow-pointer-lock allow-popups"), 
        (this.opt.className || "").split(" ").filter(function(it) {
            return it;
        }).map(function(it) {
            return root.classList.add(it);
        })), (wopt = wopt.window) && this.openWindow(wopt), this;
    }).prototype = function(obj, src) {
        var key, own = {}.hasOwnProperty;
        for (key in src) own.call(src, key) && (obj[key] = src[key]);
        return obj;
    }(Object.create(Object.prototype), {
        rpcCode: "<script>\nwindow.addEventListener(\"message\", function(e) {\nif(e.data.type == 'load') {\n  window.location.href = URL.createObjectURL(new Blob([e.data.args.content], {type: 'text/html'}));\n  return;\n}\nif(!e || !e.data || e.data.type != 'rpc') return;\nwindow[e.data.name][e.data.func](e.data.args);\n}, false);\n<\/script>",
        openWindow: function(wopt) {
            var this$ = this;
            return null == wopt && (wopt = {}), new Promise(function(res, rej) {
                var url;
                return wopt.name || (wopt.name = "sandboxjs-" + Math.random().toString(36).substring(2)), 
                url = URL.createObjectURL(new Blob([ this$.rpcCode ], {
                    type: "text/html"
                })), this$.window = window.open(url, wopt.name, "width=" + (wopt.width || 480) + ",height=" + (wopt.height || 640)), 
                this$.opt.window = wopt, this$.window.onload = function() {
                    return res();
                };
            });
        },
        send: function(msg) {
            return [ this.window, this.root ? this.root.contentWindow : null ].map(function(it) {
                if (it) return it.postMessage({
                    type: "msg",
                    payload: msg
                }, "*");
            });
        },
        setProxy: function(obj) {
            var k, v, proxy, results$ = [], this$ = this, ref$ = function() {
                var ref$, results$ = [];
                for (k in ref$ = obj) v = ref$[k], results$.push([ k, v ]);
                return results$;
            }()[0], name = ref$[0];
            for (k in obj = ref$[1], this.proxy = proxy = {}, obj) v = obj[k], results$.push(function(k) {
                return proxy[k] = function() {
                    for (var args, res$ = [], i$ = 0, to$ = arguments.length; i$ < to$; ++i$) res$.push(arguments[i$]);
                    return args = res$, [ this$.window, this$.root ? this$.root.contentWindow : null ].map(function(it) {
                        if (it) return it.postMessage({
                            type: "rpc",
                            name: name,
                            func: k,
                            args: args
                        }, "*");
                    });
                };
            }(k));
            return results$;
        },
        reload: function() {
            var this$ = this;
            return new Promise(function(res, rej) {
                var ref$;
                if (this$.root && ((ref$ = this$.root).onload = function() {
                    return res(this$.url);
                }, ref$.src = this$.url), this$.opt.window) return this$.window.postMessage({
                    type: "load",
                    args: {
                        url: this$.url,
                        content: this$.content
                    }
                });
            });
        },
        load: function(d) {
            var promises, this$ = this;
            return "string" == typeof (d = null == d ? "" : d) ? new Promise(function(res, rej) {
                return this$.content = d + this$.rpcCode, this$.url = URL.createObjectURL(new Blob([ d + this$.rpcCode ], {
                    type: "text/html"
                })), this$.reload();
            }) : (promises = [ "html", "css", "js" ].map(function(it) {
                return [ it, d[it] ];
            }).filter(function(it) {
                return it[1];
            }).map(function(n) {
                return n[1] && n[1].url ? fetch(n[1].url).then(function(v) {
                    return v && v.ok || v.clone().text().then(function(ref$) {
                        ref$ = new Error(v.status + " " + ref$);
                        throw ref$.data = v, ref$;
                    }), v.text();
                }).then(function(it) {
                    return [ n[0], it ];
                }) : Promise.resolve([ n[0], n[1] ]);
            }), Promise.all(promises).then(function(list) {
                var d = {};
                return list.map(function(it) {
                    return d[it[0]] = it[1];
                }), this$.load((d.html || "<body></body>") + "\n<script>\n//<![[CDATA\n" + d.js + '\n//]]>\n<\/script>\n<style type="text/css">\n/*<![[CDATA*/\n' + d.css + "\n/*]]>*/\n</style>");
            }));
        }
    }), "undefined" != typeof module && null !== module ? module.exports = sandbox : "undefined" != typeof window && null !== window && (window.sandbox = sandbox);
}.call(this);
