> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>react-native-turbo-log</code> </h1>
</p>

This project is based on [react-native-turbo-log](https://github.com/mattermost/react-native-turbo-log)

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-turbo-log`, The version correspondence details are as follows:

| Name    | Version    | Release Information     | Supported RN Version    | Supported Autolink     | Compile API Version     | Community Baseline Version    | npm Address                |
| ------------ | ------------ | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-turbo-log | ~0.8.0    | [Github Releases](https://github.com/react-native-oh-library/react-native-turbo-log/releases) | 0.82.* | Yes | API12+ | 0.6.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-turbo-log?activeTab=versions) |
| @react-native-ohos/react-native-turbo-log | ~0.7.0    | [Github Releases](https://github.com/react-native-oh-library/react-native-turbo-log/releases) | 0.77 | No | API12+ | 0.6.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-turbo-log?activeTab=versions) |
| @react-native-ohos/react-native-turbo-log | ~0.6.1    | [Github Releases](https://github.com/react-native-oh-library/react-native-turbo-log/releases) | 0.72 | No | API12+ | 0.6.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-turbo-log?activeTab=versions) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction：

####  npm

```bash
npm install @react-native-ohos/react-native-turbo-log
```

#### yarn


```bash
yarn add @react-native-ohos/react-native-turbo-log
```

<!-- tabs:end -->

The following code demonstrates the basic usage scenarios of this library:

> [!WARNING] The library name imported remains unchanged during usage.
### turbo_log example
``` js
import { StyleSheet, Text, View, Image, TouchableOpacity, Alert } from 'react-native';
import TurboLogger, { LogLevel } from "@react-native-ohos/react-native-turbo-log";
import { useState, useEffect } from "react"


export default function ReactNativeTurboLog() {
  useEffect(() => {
    try {
      TurboLogger.configure({
        dailyRolling: false,
        maximumFileSize: 1024 * 1024,
        maximumNumberOfFiles: 2,
      });
      Alert.alert('TurboLogger.configure Initialization successful')
    } catch (error) {
      Alert.alert('TurboLogger.configure Initialization failed', JSON.stringify(error))
    }
  }, [])

  const [result, setResult] = useState<string>();
  const [iswrite, setIswrite] = useState<boolean>(true);
  const isEmptyDataString = (data: string): boolean => {
    const trimmed = data.trim();
    return trimmed === '[]' || trimmed === '""' || trimmed === '{}';
  };

  return (
    <View style={styles.container}>
      <View><Text>The value of LogToFile is {JSON.stringify(iswrite)}</Text></View>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          setIswrite(false)
          TurboLogger.setLogToFile(false)
        }}>
        <Text>The setLogToFile property value is false</Text>
      </TouchableOpacity>
      <View><Text>The logic of the original library code is that all log methods call the write method at the end, and when the setLogToFile property value is true, the call will take effect normally</Text></View>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          setIswrite(true)
          TurboLogger.setLogToFile(true)
        }}>
        <Text>The setLogToFile property value is true</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.debug(LogLevel.Debug, 'Successfully written debug log')
        }}>
        <Text>Write debug log</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.error(LogLevel.Error, 'Successfully written error log')
        }}>
        <Text>Write error log</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.warn(LogLevel.Warning, 'Successfully written warn log')
        }}>
        <Text>Write Warning log</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.info(LogLevel.Info, 'Successfully written info log')
        }}>
        <Text>Write Info log</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          TurboLogger.log(LogLevel.Info, 'Successfully written log-info log')
        }}>
        <Text>TurboLogger. log attribute</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          const res = await TurboLogger.getLogPaths()
          if (!isEmptyDataString(JSON.stringify(res))) {
            setResult(JSON.stringify(res))
          } else {
            setResult('')
          }
        }}>
        <Text>Log path retrieval</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          const res = await TurboLogger.deleteLogs()
          if (res) {
            setResult('')
          }
        }}>
        <Text>Delete logs</Text>
      </TouchableOpacity>
      <View><Text>{result}</Text></View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: 'center',
    alignItems: 'center',
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
    marginTop: 50,
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: 'red',
    borderRadius: 5,
  },
});

```

## 2. Link

|                           | Is supported autolink | Supported RN Version |
|---------------------------|-----------------------|----------------------|
| ~0.8.0                    |  Yes              |  0.82     |
| ~0.7.0                    |  No              |  0.77     |
| ~0.6.1                    |  No             |  0.72     |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 2.1 Add overrides field to oh-package.json in the project root directory

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
}
```

 ### 2.2 There are currently two methods:

Import via har package (this method will be deprecated after the IDE improves related functions, and it is the preferred method currently);
Link source code directly.

Method 1: Import via har package (recommended)

> [!TIP] The HAR package can be found in the harmony subfolder of the third-party library's installation directory.

Open the entry/oh-package.json5 file and append the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-turbo-log": "file:../../node_modules/@react-native-ohos/react-native-turbo-log/harmony/turbo_log.har"
  }
```

Click the sync button at the top right corner.

Or run this command in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link the source code directly

> [!TIP] For direct source code linking, refer to [Direct Source Code Linking Instructions](./link-source-code.md)


### 2.3 Configure CMakeLists and import turbo_log

open entry/src/main/cpp/CMakeLists.txt，add：

```diff
include(FetchContent)
# BOOST
set(BOOST_ENABLE_CMAKE On)
FetchContent_Declare(
 Boost
 URL /7277/boost-1.82.0.tar.xz
 OVERRIDE_FIND_PACKAGE)
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)


add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-gesture-handler/src/main/cpp" ./gesture-handler)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-turbo-log/src/main/cpp" ./rnoh-turbo-log)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp") # this line is needed by codegen v1
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_gesture_handler)
+ target_link_libraries(rnoh_app PUBLIC rnoh_turbo_log)
# RNOH_END: manual_package_linking_2

```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "TurboLogPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<TurboLogPackage>(ctx),
    };
}
```

### 2.4 Import the TurboLogPackage module on the ArkTS side

open entry/src/main/ets/RNPackagesFactory.ets，add：

```diff
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+ import { TurboLogPackage } from '@react-native-ohos/react-native-turbo-log/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
return [
+    new TurboLogPackage (ctx)
  ];
 }
```

</details>

### 2.5 Run

Click the sync button in the upper right corner.

Alternatively, execute the following command in the terminal:


```bash
cd entry
ohpm install
```

Then compile and run the project.

## 3. Constraints and Limitations

### 3.1 Compatibility Support

The content of this document has been verified based on the following versions：
1. RNOH：0.72.90; SDK：HarmonyOS NEXT Developer DB3; IDE: DevEco Studio: 5.0.5.220; ROM：NEXT.0.0.105;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;
3. RNOH: 0.82.7; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.328 SP26;

## 4. Properties

> [!TIP] "Platform"This column shows which platforms the property supports in the original third-party library。

> [!TIP] "HarmonyOS Support"A value of "yes" in this column means the HarmonyOS platform supports the property; "no" means it does not; "partially" means partial support. The usage method is consistent across platforms, and the effect is comparable to that on iOS or Android。

**Turbo_log**：A feature for log storage, retrieving log paths, and deleting logs

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| configure | Initialize Configuration     | function | no       | Android | yes               |
| deleteLogFiles | Delete All Logs     | function | no       | Android | yes               |
| getLogFilePaths | Return All Log Paths     | function | no       | Android | yes               |
| setLogToFile | Turn on/off logging to files     | function | no       | Android | yes               |
| debug | Encapsulate TurboLogger.debug     | function | no       | Android | yes               |
| error | Encapsulate TurboLogger.error     | function | no       | Android | yes               |
| warn | Encapsulate TurboLogger.warn     | function | no       | Android | yes               |
| info | EncapsulateTurboLogger.info     | function | no       | Android | yes               |
| log | Print logs for judgment/condition checks     | function | no       | Android | yes               |

## 5. Static Method

## 6. Pending Issues

## 7. Others

## 8. Open Source License

This project is based on [The MIT License (MIT)](https://github.com/mattermost/react-native-turbo-log/blob/master/LICENSE) ，Feel free to enjoy and contribute to the open source project。
