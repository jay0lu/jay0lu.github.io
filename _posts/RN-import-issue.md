You can mix require and export. You can't mix import and module.exports.

'This issue was newly affecting me after instructing Babel to not transpile module syntax. As sokra described, it only occurred when trying to use CommonJS style module.exports inside of ES modules. require always works. This can be fixed by simply replacing all module.exports = ... to export default ... where applicable, as this is seemingly equivalent for old Babel-style ES module transpilation. (Note though, that importing this module using require will probably give you an option with a default key rather than the default export itself, so it's probably best you make the switch across the entire codebase at once.)'
https://github.com/webpack/webpack/issues/4039
