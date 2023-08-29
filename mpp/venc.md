# 编码结构化设计
## 抽象API
没有使用c++的抽象编码,采用传统的c实现的抽象接口, 对应的抽象化文件:enc_impl_api.h
```
typedef struct EncImplApi_t {
    char            *name;							//实例化的模块名字,编码实例包含264/265/JPEG/VP8等
    MppCodingType   coding;							//编码类型
    RK_U32          ctx_size;						//实例化的接口大小
    RK_U32          flag;			

    MPP_RET (*init)(void *ctx, EncImplCfg *ctrlCfg);
    MPP_RET (*deinit)(void *ctx);

    MPP_RET (*proc_cfg)(void *ctx, MpiCmd cmd, void *param);
    MPP_RET (*gen_hdr)(void *ctx, MppPacket pkt);

    MPP_RET (*start)(void *ctx, HalEncTask *task);
    MPP_RET (*proc_dpb)(void *ctx, HalEncTask *task);
    MPP_RET (*proc_hal)(void *ctx, HalEncTask *task);

    MPP_RET (*add_prefix)(MppPacket pkt, RK_S32 *length, RK_U8 uuid[16],
                          const void *data, RK_S32 size);

    MPP_RET (*sw_enc)(void *ctx, HalEncTask *task);
} EncImplApi;
```

## 实例化 
```
const EncImplApi api_vp8e = {/*api_vp8e 实例化*/
    .name       = "vp8_control",
    .coding     = MPP_VIDEO_CodingVP8,
    .ctx_size   = sizeof(Vp8eCtx),
    .flag       = 0,
    .init       = vp8e_init,
    .deinit     = vp8e_deinit,
    .proc_cfg   = vp8e_proc_cfg,
    .gen_hdr    = NULL,
    .start      = vp8e_start,
    .proc_dpb   = vp8e_proc_dpb,
    .proc_hal   = vp8e_proc_hal,
    .add_prefix = NULL,
    .sw_enc     = NULL,
};


```
## 实例化选择
```
static const EncImplApi *enc_apis[] = {
#if HAVE_H264E
    &api_h264e,
#endif
#if HAVE_H265E
    &api_h265e,
#endif
#if HAVE_JPEGE
    &api_jpege,
#endif
#if HAVE_VP8E
    &api_vp8e,
#endif
};
```