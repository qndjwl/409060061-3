var transpiler;
window.transpiler = transpiler = {
  livescript: {
    destype: 'javascript',
    test: function(v){
      v == null && (v = '');
      return (typeof lsc != 'undefined' && lsc !== null) && v.startsWith('#- lsc');
    },
    transform: function(v){
      v == null && (v = '');
      return lsc.compile(v, {
        bare: true,
        header: false
      });
    }
  },
  pug: {
    destype: 'html',
    test: function(v){
      v == null && (v = '');
      return (typeof pug != 'undefined' && pug !== null) && v.startsWith('//- pug');
    },
    transform: function(v){
      v == null && (v = '');
      return pug.render(v, {
        filename: 'index.pug',
        basedir: '.'
      });
    }
  },
  markdown: {
    destype: 'html',
    test: function(v){
      v == null && (v = '');
      return (typeof marked != 'undefined' && marked !== null) && v.startsWith('<!-- md -->');
    },
    transform: function(v){
      v == null && (v = '');
      return marked(v);
    }
  },
  stylus: {
    destype: 'css',
    test: function(v){
      v == null && (v = '');
      return (typeof stylus != 'undefined' && stylus !== null) && v.startsWith('//- stylus');
    },
    transform: function(v){
      v == null && (v = '');
      return stylus.render(v);
    }
  }
};