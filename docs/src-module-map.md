# OpenCAMLib `/src` module map

- **`src/algo`**
  - **Responsibility (1 sentence):** Implements core CAM toolpath algorithms and orchestration primitives (`Operation`) for waterline, weave, zigzag, and push-cutter workflows.  
  - **Public entry headers:** `operation.hpp`, `waterline.hpp`, `adaptivewaterline.hpp`, `batchpushcutter.hpp`, `fiberpushcutter.hpp`, `weave.hpp`, `zigzag.hpp`.  
  - **Key types (top 5):** `Operation`, `Waterline`, `AdaptiveWaterline`, `BatchPushCutter`, `weave::Weave`.  
  - **Key algorithms (top 5):** `Waterline::run`, `AdaptiveWaterline::adaptive_sampling_run`, `BatchPushCutter::pushCutter3`, `FiberPushCutter::pushCutter2`, `Weave::face_traverse`.

- **`src/common`**
  - **Responsibility (1 sentence):** Provides shared numeric, filtering, graph, and spatial indexing utilities used by higher-level cutting/toolpath modules.  
  - **Public entry headers:** `numeric.hpp`, `kdtree.hpp`, `kdnode.hpp`, `clfilter.hpp`, `lineclfilter.hpp`, `halfedgediagram.hpp`, `brent_zero.hpp`.  
  - **Key types (top 5):** `KDTree<BBObj>`, `KDNode<BBObj>`, `CLFilter`, `LineCLFilter`, `HEDIGraph`.  
  - **Key algorithms (top 5):** `KDTree::build`, `KDTree::search`, `LineCLFilter::run`, `brent_zero`, `two_by_two_solver`.

- **`src/cutters`**
  - **Responsibility (1 sentence):** Defines milling cutter geometry/kinematics and contact algorithms for drop/push-cutter collision tests against triangle meshes.  
  - **Public entry headers:** `millingcutter.hpp`, `ballcutter.hpp`, `bullcutter.hpp`, `conecutter.hpp`, `cylcutter.hpp`, `compositecutter.hpp`, `ellipse.hpp`, `ellipseposition.hpp`.  
  - **Key types (top 5):** `MillingCutter`, `BallCutter`, `BullCutter`, `ConeCutter`, `CompositeCutter`.  
  - **Key algorithms (top 5):** `MillingCutter::dropCutter`, `MillingCutter::pushCutter`, `MillingCutter::facetDrop`, `CompositeCutter::edgeDrop`, `CompositeCutter::facetPush`.

- **`src/dropcutter`**
  - **Responsibility (1 sentence):** Implements drop-cutter operations over single points, point batches, and sampled/adaptive paths on STL surfaces.  
  - **Public entry headers:** `pointdropcutter.hpp`, `batchdropcutter.hpp`, `pathdropcutter.hpp`, `adaptivepathdropcutter.hpp`.  
  - **Key types (top 5):** `PointDropCutter`, `BatchDropCutter`, `PathDropCutter`, `AdaptivePathDropCutter`, `Operation` (base).  
  - **Key algorithms (top 5):** `BatchDropCutter::dropCutter5`, `PathDropCutter::uniform_sampling_run`, `PathDropCutter::sample_span`, `AdaptivePathDropCutter::adaptive_sample`, `PointDropCutter::pointDropCutter1`.

- **`src/geo`**
  - **Responsibility (1 sentence):** Provides geometric primitives, mesh containers, and path/span abstractions consumed by cutters and algorithms.  
  - **Public entry headers:** `point.hpp`, `line.hpp`, `arc.hpp`, `path.hpp`, `triangle.hpp`, `bbox.hpp`, `stlsurf.hpp`, `stlreader.hpp`, `clpoint.hpp`, `ccpoint.hpp`.  
  - **Key types (top 5):** `Point`, `Triangle`, `STLSurf`, `Path`, `Bbox`.  
  - **Key algorithms (top 5):** `Point::closestPoint`, `Point::isInside`, `Triangle::zslice_verts`, `Bbox::overlaps`, `STLReader::read_from_file`.

- **`src/pythonlib`**
  - **Responsibility (1 sentence):** Exposes OpenCAMLib C++ types/algorithms to Python via Boost.Python and wrapper adapter classes.  
  - **Public entry headers:** `millingcutter_py.hpp`, `fiber_py.hpp`, `pathdropcutter_py.hpp`, `waterline_py.hpp`, `batchdropcutter_py.hpp`, `adaptivepathdropcutter_py.hpp`, `weave_py.hpp`.  
  - **Key types (top 5):** `MillingCutter_py`, `Fiber_py`, `PathDropCutter_py`, `Waterline_py`, `weave::Weave_py`.  
  - **Key algorithms (top 5):** `BOOST_PYTHON_MODULE(ocl)`, `export_algo`, `export_dropcutter`, `MillingCutter_py::vertexDrop`, `Weave_py::py_getLoops`.

- **`src/nodejslib`**
  - **Responsibility (1 sentence):** Implements Node-API wrappers for geometry, cutter, and algorithm classes and registers them into the Node addon entrypoint.  
  - **Public entry headers:** `nodejslib.cpp`, `waterline_js.hpp`, `adaptivewaterline_js.hpp`, `pathdropcutter_js.hpp`, `adaptivepathdropcutter_js.hpp`, `stlsurf_js.hpp`, `point_js.hpp`.  
  - **Key types (top 5):** `WaterlineJS`, `AdaptiveWaterlineJS`, `PathDropCutterJS`, `STLSurfJS`, `PointJS`.  
  - **Key algorithms (top 5):** `InitAll`, `WaterlineJS::run`, `AdaptiveWaterlineJS::getLoops`, `PathDropCutterJS::getCLPoints`, `STLReaderJS::Init`.

- **`src/emscriptenlib`**
  - **Responsibility (1 sentence):** Declares WebAssembly/JS bindings for core geometry, cutter, and CAM algorithm APIs through Emscripten embind.  
  - **Public entry headers:** `emscriptenlib.cpp` (single binding entry translation unit).  
  - **Key types (top 5):** `Point` (bound), `STLSurf` (bound), `BatchDropCutter` (bound), `PathDropCutter` (bound), `AdaptiveWaterline` (bound).  
  - **Key algorithms (top 5):** `EMSCRIPTEN_BINDINGS(opencamlib)`, `class_<BatchDropCutter>(...).function("run", &BatchDropCutter::run)`, `class_<PathDropCutter>(...).function("run", &PathDropCutter::run)`, `class_<AdaptivePathDropCutter>(...).function("run", &AdaptivePathDropCutter::run)`, `class_<AdaptiveWaterline>(...).function("run", &AdaptiveWaterline::run)`.

- **`src/cxxlib`**
  - **Responsibility (1 sentence):** CMake packaging hook for exporting/building the native C++ library target(s), not a source module with headers/classes itself.  
  - **Public entry headers:** none in this folder (`cxxlib.cmake` only).  
  - **Key types (top 5):** none declared in this folder.  
  - **Key algorithms (top 5):** none declared in this folder.

- **`src/deb`**
  - **Responsibility (1 sentence):** Debian packaging metadata and CMake fragments for generating distro packages rather than runtime APIs.  
  - **Public entry headers:** none in this folder (packaging text/CMake only).  
  - **Key types (top 5):** none declared in this folder.  
  - **Key algorithms (top 5):** none declared in this folder.

- **`src/npmpackage`**
  - **Responsibility (1 sentence):** TypeScript npm package scaffold that wraps/distributes JS-facing OpenCAMLib interfaces (`package.json`, TS source, tests).  
  - **Public entry headers:** none (`.ts`/`package.json` module boundary, not C++ headers).  
  - **Key types (top 5):** TypeScript-side `Point`, `Path`, `STLSurf`, `Triangle`, `MillingCutter` classes/interfaces.  
  - **Key algorithms (top 5):** package entry re-exports in `src/index.d.ts` plus TypeScript method implementations in wrapper classes.
