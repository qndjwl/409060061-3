var pug, lsc;
window.pug = pug = require("pug");
window.lsc = lsc = require("livescript");
window.renderer = function(data, sandbox, opt){
  var payload;
  opt == null && (opt = {});
  payload = {};
  ['html', 'css', 'js'].map(function(it){
    return payload[it] = data["index." + it];
  });
  if (transpiler.pug.test(payload.html)) {
    payload.html = transpiler.pug.transform(payload.html);
  }
  if (transpiler.livescript.test(payload.js)) {
    payload.js = transpiler.livescript.transform(payload.js);
  }
  if (transpiler.stylus.test(payload.css)) {
    payload.css = transpiler.stylus.transform(payload.css);
  }
  if (opt.fontSize) {
    payload.css = ("html { font-size: " + opt.fontSize + " }") + payload.css;
  }
  return sandbox.load(payload);
};