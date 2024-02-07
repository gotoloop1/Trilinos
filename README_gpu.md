# Trilinos を GPU に対応させてビルドするための情報

## (wisteria にて) OpenBLAS をビルドする

```sh
make CC=mpicc CXX=mpic++ FC=mpif90
make install PREFIX=OpenBLASをインストールする場所
```

## コンパイル・インストール

- OpenACC, OpenMP を使用 (括弧の中は wisteria では必要)

```sh
mkdir build
cd build
CC=nvc CXX=nvc++ FC=nvfortran cmake (-DBLAS_LIBRARY_DIRS='OpenBLASをインストールした場所/lib' -DBLAS_LIBRARY_NAMES=openblas -DLAPACK_LIBRARY_DIRS='OpenBLASをインストールした場所/lib' -DLAPACK_LIBRARY_NAMES=openblas) -DCMAKE_INSTALL_PREFIX='Trilinosをインストールする場所' -DTrilinos_ENABLE_ML=ON -DTrilinos_ENABLE_OpenMP=ON -DCMAKE_C_FLAGS='-acc -Minfo=accel -gpu=managed' -DCMAKE_CXX_FLAGS='-acc -Minfo=accel -gpu=managed' -DCMAKE_BUILD_TYPE=NONE ..
make -j
make install
```

- OpenACC, OpenMP, MPI を使用 (括弧の中は wisteria では必要)

```sh
mkdir build
cd build
CC=mpicc CXX=mpic++ FC=mpif90 cmake (-DBLAS_LIBRARY_DIRS='OpenBLASをインストールした場所/lib' -DBLAS_LIBRARY_NAMES=openblas -DLAPACK_LIBRARY_DIRS='OpenBLASをインストールした場所/lib' -DLAPACK_LIBRARY_NAMES=openblas) -DCMAKE_INSTALL_PREFIX='Trilinosをインストールする場所' -DTrilinos_ENABLE_ML=ON -DTrilinos_ENABLE_OpenMP=ON -DTPL_ENABLE_MPI=ON -DTrilinos_ENABLE_MPI=ON -DCMAKE_C_FLAGS='-acc -Minfo=accel -gpu=managed' -DCMAKE_CXX_FLAGS='-acc -Minfo=accel -gpu=managed' -DCMAKE_BUILD_TYPE=NONE ..
make -j
make install
```
