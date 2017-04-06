# Installation of PIPS-NLP and Julia/StructJuMP

1. Clone the latest PIPS version.
```bash
git clone https://github.com/michel2323/PIPS.git
```
2. Be sure to have optained a licensed [ma57 library](http://www.hsl.rl.ac.uk/catalogue/ma57.html) tarball and place it in your MA57 folder.
```bash
mv ma57-3.9.0.tar.gz ThirdPartyLibs/MA57
```
3. Build third party libraries. Adapt script if needed.

```bash
./build_3rdparty.sh
```
4. Setup PIPS-NLP:
```bash
mkdir build
cd build
cmake -DCMAKE_BUILD_TYPE=RELEASE -DBUILD_ALL=OFF -DBUILD_PIPS_NLP=ON -DBUILD_PIPS_DOC=ON -DDUMP=ON -B. -H..
```
   This creates a build setup for PIPS that dumps 1st stage matrices, creates a doxygen makefile target to generate the documentation, and only builds PIPS-NLP. Change the build options to your needs.
5. Build PIPS-NLP with 4 threads:
```bash
make -j4
```
6. Download and install Julia 0.4.7 (support for 0.5 is in the works).
7. Clone StructJuMP:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMP.jl.git")
```
8. Clone the StructJuMP solver interface:
```julia
Pkg.clone("https://github.com/StructJuMP/StructJuMPSolverInterface.jl")
```
9. In  ~/.julia/v0.4/StructJUMP/StructJuMP.jl manually disable precompilation, and import StructJuMPSolverInterface and MPI.

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
10. Export the location of the PIPS library to StructJuMP. It is advised to put these lines in your .bashrc.
```bash
export PIPS_NLP_SHARED_LIB=$YOUR_PIPS_FOLDER/build/PIPS-NLP/libpipsnlp.so
export PIPS_NLP_PAR_SHARED_LIB=$YOUR_PIPS_FOLDER/build/PIPS-NLP/libparpipsnlp.so
```
