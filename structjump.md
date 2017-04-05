# Installation of PIPS-NLP and Julia/StructJuMP

1. Build third party libraries:

```bash
./build_3rdparty.sh
```
2. Build PIPS-NLP:
```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RELEASE -DBUILD_ALL=OFF -DBUILD_PIPS_NLP=ON -DBUILD_PIPS_DOC=ON -DDUMP=ON -B. -H..
```
   This creates a version of pips that dumps 1st stage matrices, creates a doxygen makefile target to generate the documentation, and only build PIPS-NLP.
3. Download and install Julia 0.4.7 (support for 0.5 is in the works).
4. Clone StructJuMP:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMP.jl.git")
```
5. Clone the StructJuMP solver interface:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMPSolverInterface.jl")
```
6. In  ~/.julia/v0.4/StructJUMP/StructJuMP.jl manually disable precompilation, and import StructJuMPSolverInterface and MPI.

```diff
--- a/src/StructJuMP.jl
+++ b/src/StructJuMP.jl
@@ -1,4 +1,4 @@
-__precompile__()
+#__precompile__()
 
module StructJuMP
   
@@ -7,8 +7,8 @@ 
import MathProgBase
import ReverseDiffSparse
     
# These modules could be optional.
-# import StructJuMPSolverInterface
-# import MPI
+import StructJuMPSolverInterface
+import MPI
```

