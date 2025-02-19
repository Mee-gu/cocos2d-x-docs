## Optimizations for OPPO devices

 > Note: This document applies to __Cocos2d-x 3.17.2__ and later only.
 __Cocos2d-x__ has a few optimizations for __OPPO__ devices. These optimizations will only work on __OPPO__ devices (specially Reno devices currently) . 

### What's optimized
There are two places that are optimized:

  * load a scene
  * engine's internal shaders compiling

Loading scene optimizations start when `Scene` is created, and ended in `Scene::onEnter()` and therefore you should create resources between them.

### Invoke optimization codes manually
The application knows where more power is needed, better than engine knows. You can invoke this API to get more power when needed. You can invoke the API in both C++ or Java.

#### Example usage in C++

```c++
// Scene loading starts, need more power.
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onSceneLoaderBegin();
#end if

// Scene loading ends.
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onSceneLoaderEnd();
#end if

// Shader compiling begin, need more power.
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onShaderLoaderBegin();
#end if

// Shader compiling ends.
#if CC_TARGET_PLATFORM == CC_PLATFORM_ANDROID
    DataManager::onShaderLoaderEnd();
#end if
```

#### Example usage in Java:

```Java
Cocos2dxDataManager::setOptimise(String thing, float value);
```

#### Table Of Values
| item | 1 | 0 |
| ----  | -- | -- |
| load_scene| start | end |
| shader_compile | start | end |

After v3.17.2, the type of `value` changed from `float` to `string` to make it more freshable.

