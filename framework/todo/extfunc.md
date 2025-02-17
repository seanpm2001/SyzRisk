### Replacing the function extractor and the diff-level engine to a nicer version.

`extfunc` is a script responsible for extracting functions from source code. The current implementation is quite _horrible_, to say the least, riddled with a ton of heuristics and even Linux-specific corner case handling. While I wouldn't bother to change it if it's working fine, but unfortunately, it isn't sometimes; it only works decently well for the Linux kernel code, and sometimes it takes forever if the source size is enormous.

Fortunately, replacing it is pretty straightforward. We can either improve or rewrite the script or, if we're not bothered to use another tool, we can even use Clang's AST generation, extract the ASTs of individual functions, and _pretty-print_ it to convert back ASTs to source code. All these things are engineering work, but hey. It should be fun. (weekend project?)

A similar issue is also in the diff-level matcher, which scans a diff file in a kind of dumb way; if it takes forever, some dates may need to be explicitly skipped. This can also presumably be resolved with some technical work by de-dumbifying the scanning loop.
