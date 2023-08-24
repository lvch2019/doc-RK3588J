# 编码结构化设计
没有使用c++的抽象编码,采用传统的c实现的IMPL方式
```
typedef struct EncImplApi_t {
    char            *name;
    MppCodingType   coding;
    RK_U32          ctx_size;
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