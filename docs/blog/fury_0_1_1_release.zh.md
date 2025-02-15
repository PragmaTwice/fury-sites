# Fury v0.1.1 released

Author: [chaokunyang](https://github.com/chaokunyang)

I'm pleased to announce the `0.1.1` release of Fury. This release is a enhanced verson based on fury `0.1.0`. It keeps binary compatibility with `0.1.0`.


## Highlights
- Java
  - Dubbo fury integration: https://github.com/fury-project/dubbo-serialization-fury
  -  Add class checker API to customize security check behaviour(#890)
- Python
  - Support pyarrow6 bazel build (#859 #862)
  - Support python 3.10 (#859 #862)
## What's Changed
- [Java] Dubbo fury integration: https://github.com/fury-project/dubbo-serialization-fury
- [Java] fix isSecure check for xlang in java (#822)
- [Java] register empty object by default (#829)
- [Java] upgrade guava for(#831)
- [Python] Support pyarrow6 bazel build (#859)
- [Python] add missing shared lib for python (#862)
- [Java] optimize buffer copy (#870)
- [Doc] Fix row format doc (#873)
- [Java] fix ofHashMap (#877)
- [Java] add jdk tools.jar for tests (#881)
- [Java] Fix lazy bean serializer (#883)
- [Java] print exception for fury creation (#885)
- [Java] remove getCurrentFury API (#887)
- [Java] Add fury map iterator api (#889)
- [Java] Add class checker API (#890)
- [Python] Fix python linux deploy missing shared library files (#892)
- [[Java] refine AllowListChecker (#893)

**Full Changelog**: https://github.com/alipay/fury/compare/v0.1.0...v0.1.1