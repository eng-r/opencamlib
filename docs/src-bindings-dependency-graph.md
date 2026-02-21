# `src` module dependency graph (core + bindings)

This graph is derived from C/C++ `#include` relationships in `src/*`.

## Nodes
- Core modules: `geo`, `common`, `cutters`, `algo`, `dropcutter`
- Binding modules: `pythonlib`, `nodejslib`, `emscriptenlib`

## Directed edges with include evidence

- `algo -> common` via `#include "kdtree.hpp"` in `src/algo/batchpushcutter.hpp:31`.
- `algo -> cutters` via `#include "millingcutter.hpp"` in `src/algo/waterline.cpp:28`.
- `algo -> geo` via `#include "point.hpp"` in `src/algo/fiberpushcutter.hpp:29`.

- `common -> cutters` via `#include "millingcutter.hpp"` in `src/common/kdtree.hpp:32`.
- `common -> geo` via `#include "point.hpp"` in `src/common/numeric.hpp:26`.

- `cutters -> algo` via `#include "fiber.hpp"` in `src/cutters/ellipse.cpp:31`.
- `cutters -> common` via `#include "numeric.hpp"` in `src/cutters/bullcutter.cpp:28`.
- `cutters -> geo` via `#include "point.hpp"` in `src/cutters/ellipseposition.cpp:28`.

- `dropcutter -> algo` via `#include "operation.hpp"` in `src/dropcutter/pointdropcutter.hpp:31`.
- `dropcutter -> common` via `#include "kdtree.hpp"` in `src/dropcutter/pointdropcutter.hpp:30`.
- `dropcutter -> cutters` via `#include "millingcutter.hpp"` in `src/dropcutter/pointdropcutter.hpp:29`.
- `dropcutter -> geo` via `#include "clpoint.hpp"` in `src/dropcutter/pointdropcutter.hpp:28`.

- `geo -> common` via `#include "numeric.hpp"` in `src/geo/point.cpp:27`.

- `pythonlib -> algo` via `#include "waterline.hpp"` in `src/pythonlib/waterline_py.hpp:28`.
- `pythonlib -> common` via `#include "lineclfilter.hpp"` in `src/pythonlib/lineclfilter_py.hpp:27`.
- `pythonlib -> cutters` via `#include "millingcutter.hpp"` in `src/pythonlib/ocl_cutters.cpp:24`.
- `pythonlib -> dropcutter` via `#include "batchdropcutter.hpp"` in `src/pythonlib/batchdropcutter_py.hpp:27`.
- `pythonlib -> geo` via `#include "stlsurf.hpp"` in `src/pythonlib/stlsurf_py.hpp:27`.

- `nodejslib -> algo` via `#include "waterline.hpp"` in `src/nodejslib/waterline_js.hpp:2`.
- `nodejslib -> cutters` via `#include "ballcutter.hpp"` in `src/nodejslib/ballcutter_js.hpp:2`.
- `nodejslib -> dropcutter` via `#include "adaptivepathdropcutter.hpp"` in `src/nodejslib/adaptivepathdropcutter_js.hpp:2`.
- `nodejslib -> geo` via `#include "bbox.hpp"` in `src/nodejslib/bbox_js.cpp:1`.

- `emscriptenlib -> algo` via `#include "operation.hpp"` in `src/emscriptenlib/emscriptenlib.cpp:20`.
- `emscriptenlib -> common` via `#include "lineclfilter.hpp"` in `src/emscriptenlib/emscriptenlib.cpp:27`.
- `emscriptenlib -> cutters` via `#include "ellipse.hpp"` in `src/emscriptenlib/emscriptenlib.cpp:12`.
- `emscriptenlib -> dropcutter` via `#include "adaptivepathdropcutter.hpp"` in `src/emscriptenlib/emscriptenlib.cpp:22`.
- `emscriptenlib -> geo` via `#include "point.hpp"` in `src/emscriptenlib/emscriptenlib.cpp:5`.

## Cycles

Strongly connected component among core modules:
- `{algo, common, cutters, geo}`

Direct/back edges that create cycles:
- `algo -> cutters` and `cutters -> algo`
- `common -> cutters` and `cutters -> common`
- `common -> geo` and `geo -> common`
- plus longer loops such as `algo -> geo -> common -> cutters -> algo`

`dropcutter` and all bindings are acyclic consumers in this graph (only outgoing edges to core modules).
