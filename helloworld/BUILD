# Copyright 2020 Pants project contributors.
# Licensed under the Apache License, Version 2.0 (see LICENSE).

python_library(
    name='multi-deployable-main',
    sources=["main.py"],
    # Dependencies inferred from main.py.
)

python_binary(
    # name defaults to the name of this directory, i.e., `helloworld`.
    entry_point="helloworld.main",
    dependencies=[':multi-deployable-main'],
)

python_binary(
    name="helloworld-awslambda",
    entry_point="helloworld.awslambda:handler",
    dependencies=[':multi-deployable-main'],
    # Note: Has sdist dependencies, so must be built on Linux.
    platforms=['linux_x86_64-cp-37-m'],
)

python_binary(
    name="helloworld_py2",
    sources=["main_py2.py"],
    entry_point="helloworld.main_py2",
    compatibility=">=2.7,<3",
)

python_library(
    name="config",
    sources=["config.py"],
    dependencies=[
        # Pants cannot infer dependencies on resources targets and Protobuf, so we explicitly
        # add them.
        ":config_file",
        "helloworld/util/proto",
    ],
)

resources(
    name="config_file",
    sources=["config.json"],
)
