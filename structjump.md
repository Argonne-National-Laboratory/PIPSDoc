# Installation of PIPS-NLP and Julia/StructJuMP

1. Build third party libraries and PIPS-NLP
2. Download and install Julia 0.4.7 (support for 0.5 is in the works).
3. Clone StructJuMP:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMP.jl.git")
```
4. Clone the StructJuMP solver interface:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMPSolverInterface.jl")
```
5. In  ~/.julia/v0.4/StructJUMP/StructJuMP.jl manually disable precompilation, and import StructJuMPSolverInterface and MPI.

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

