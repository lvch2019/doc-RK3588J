# VPSS
VPSS（Video Process Sub-System）是视频处理子系统，支持的具体图像处理功能包括CROP、Scale、像素格式转换、固定角
度旋转、Cover/Coverex、Mirror/Flip、压缩解压等。

## GROUP
1. 最大值VPSS_MAX_GRP_NUM	(256)
2. 各GROUP分时复用硬件设置,硬件依次处理各组提交德任务。 

## CHANNEL
GROUP组的通道。提供多个通道,每个通道具有缩放,裁剪等功能。把图像裁剪,缩放成用户设置的目标分辨率输出。

## VPSS API 流程(VI->VPSS->VENC)

### 1. 创建通道组 
```
RK_S32 RK_MPI_VPSS_CreateGrp(VPSS_GRP VpssGrp/*0*/, const VPSS_GRP_ATTR_S *pstGrpAttr);
```
### 2. 设置通道属性
```
					/*		通道组*/		通道序号*/			通道属性*/
RK_MPI_VPSS_SetChnAttr(VPSS_GRP VpssGrp, VPSS_CHN VpssChn, const VPSS_CHN_ATTR_S *pstChnAttr);
```
### 3. 使能通道
```
RK_S32 RK_MPI_VPSS_EnableChn(VPSS_GRP VpssGrp, VPSS_CHN VpssChn);
```

### 4. 使能Backup帧
```
RK_MPI_VPSS_EnableBackupFrame(VPSS_GRP VpssGrp);
```
### 5. 
```
RK_S32 RK_MPI_VPSS_StartGrp(VPSS_GRP VpssGrp);
```

### 6. VI->VPSS 
```
 // bind vi to vpss
    stViChn.enModId    = RK_ID_VI;
    stViChn.s32DevId   = ctx->devId;
    stViChn.s32ChnId   = ctx->channelId;
    stVpssChn.enModId = RK_ID_VPSS;
    stVpssChn.s32DevId = 0;
    stVpssChn.s32ChnId = 0;

    RK_LOGD("vi to vpss ch %d vpss group %d", stVpssChn.s32ChnId , stVpssChn.s32DevId);
    s32Ret = RK_MPI_SYS_Bind(&stViChn, &stVpssChn);
    if (s32Ret != RK_SUCCESS) {
        RK_LOGE("vi and vpss bind error ");
        goto __FAILED;
    }

```
