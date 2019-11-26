Bootstrap: docker
From: julia:1.2.0

%help
    Julia 1.2 docker image

%environment
    export JULIA_DEPOT_PATH=/opt/julia
    export JULIA_PKGDIR=/opt/julia
    export JULIA_VERSION=1.2.0
    export JULIA_PATH=/usr/local/julia
    export PATH=$JULIA_PATH/bin:$PATH
    export COMPILEFOLDER=/opt/julia/compiled/v1.2/
    export LC_ALL=C.UTF-8
    export LANG=C.UTF-8

%post
    locale-gen --purge en_US.UTF-8
    echo -e 'LANG="en_US.UTF-8"\nLANGUAGE="en_US:en"\n' > /etc/default/locale
    
    chmod -R 0755 /opt
    chmod -R 0755 /usr/local/julia

    JULIA_DEPOT_PATH=/opt/julia
    JULIA_PKGDIR=/opt/julia
    JULIA_VERSION=1.2.0

    JULIA_PATH=/usr/local/julia
    PATH=$JULIA_PATH/bin:$PATH

    mkdir -p "$JULIA_DEPOT_PATH"

    julia -e 'using Pkg; Pkg.add(["Dates", "Parsers", "PooledArrays", "WeakRefStrings", "FilePathsBase", "LazyArrays", "Libdl", "Mmap", "CategoricalArrays", "Missings", "InvertedIndices", "Tables", "TableTraits", "IteratorInterfaceExtensions", "DataAPI", "Unicode", "SortingAlgorithms", "Reexport", "TextWrap", "Compat", "Blosc", "ArgParse", "DataFrames", "CSV", "Profile", "Random", "Statistics", "HDF5"])'

    COMPILEFOLDER=/opt/julia/compiled/v1.2/

    mkdir -p "$COMPILEFOLDER/ArgParse" && \
    mkdir -p "$COMPILEFOLDER/HDF5" && \
    mkdir -p "$COMPILEFOLDER/Profile" && \
    mkdir -p "$COMPILEFOLDER/DataFrames" && \
    mkdir -p "$COMPILEFOLDER/CSV" && \
    mkdir -p "$COMPILEFOLDER/Statistics"

    julia -e "Base.compilecache(Base.PkgId(\"ArgParse\"))" && \
    julia -e "Base.compilecache(Base.PkgId(\"HDF5\"))" && \
    julia -e "Base.compilecache(Base.PkgId(\"Profile\"))" && \
    julia -e "Base.compilecache(Base.PkgId(\"DataFrames\"))" && \
    julia -e "Base.compilecache(Base.PkgId(\"CSV\"))" && \
    julia -e "Base.compilecache(Base.PkgId(\"Statistics\"))"

%runscript
    exec julia "$@"

# %startscript
# exec /bin/bash julia "$@"
