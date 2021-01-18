# xocl_kernel5.4
make the xrt 2019.1 xocl driver support kernel 5.4 

###### remove the qdma subdevice
###### remove the xvc subdevice


###### change the vendid form 1ded to 10ee fit for u200
###### change the device number from 1004 to 5001 --fit for u200
###### change the MODULE_AUTHOR("MinX <For_test@Aliyun.com>")--for debug use

DRM API change

#if LINUX_VERSION_CODE >= KERNEL_VERSION(5,7,0)
        #define XOCL_DRM_GEM_OBJECT_PUT_UNLOCKED drm_gem_object_put
        #define XOCL_DRM_GEM_OBJECT_GET drm_gem_object_get
#elif LINUX_VERSION_CODE >= KERNEL_VERSION(4,12,0)
        #define XOCL_DRM_GEM_OBJECT_PUT_UNLOCKED drm_gem_object_put_unlocked
        #define XOCL_DRM_GEM_OBJECT_GET drm_gem_object_get
#elif defined(RHEL_RELEASE_CODE)
        #if RHEL_RELEASE_CODE >= RHEL_RELEASE_VERSION(7,5)
                #define XOCL_DRM_GEM_OBJECT_PUT_UNLOCKED drm_gem_object_put_unlocked
                #define XOCL_DRM_GEM_OBJECT_GET drm_gem_object_get
        #else
                #define XOCL_DRM_GEM_OBJECT_PUT_UNLOCKED drm_gem_object_unreference_unlocked
                #define XOCL_DRM_GEM_OBJECT_GET drm_gem_object_reference
        #endif
#else
        #define XOCL_DRM_GEM_OBJECT_PUT_UNLOCKED drm_gem_object_unreference_unlocked
        #define XOCL_DRM_GEM_OBJECT_GET drm_gem_object_reference
#endif

