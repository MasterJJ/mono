
# Runtime debugging

- Use the debug version of the runtime from builds/debug. This can be done by using the '--debugrt' option in the packager.
- Disable symbol stripping by using the '--no-native-strip' option in the packager.
- Emscripten generates dwarf debug info and Chrome 80 and later can use it.
- To break in the JS debugger from runtime code, do:
```
#include <emscripten.h>  
EM_ASM(debugger;);
```
- To print a stack trace from runtime code, do:
```
#include <emscripten.h>  
EM_ASM(
	var err = new Error();
	console.log ("Stacktrace: \n");
	console.log (err.stack);
);
```
- The runtime-tests.js test runner supports various options useful for debugging:
   - Runtime command line options can be passed using the --runtime-arg=<arg> option.
      In particular --trace can be used to enable executing tracing when using the interpreter.
  - Environment variables can be set using --setenv=<var>=<value>
     In particular MONO_LOG_LEVEL/MONO_LOG_MASK can be set.
- The --stack-trace-limit=1000 option to V8 can be used to avoid V8 truncating stack traces.

