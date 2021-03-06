---
title: ICorDebugProcess2::SetUnmanagedBreakpoint 方法
ms.date: 03/30/2017
api_name:
- ICorDebugProcess2.SetUnmanagedBreakpoint
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint
helpviewer_keywords:
- ICorDebugProcess2::SetUnmanagedBreakpoint method [.NET Framework debugging]
- SetUnmanagedBreakpoint method [.NET Framework debugging]
ms.assetid: 93829d15-d942-4e2d-b7a4-dfc9d7fb96be
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: d4326c6d8a3ee780cf63652badc8c527f55a075c
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33420812"
---
# <a name="icordebugprocess2setunmanagedbreakpoint-method"></a>ICorDebugProcess2::SetUnmanagedBreakpoint 方法
指定的本机映像的偏移量处设置非托管的断点。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT SetUnmanagedBreakpoint (  
    [in]  CORDB_ADDRESS    address,  
    [in]  ULONG32          bufsize,  
    [out, size_is(bufsize), length_is(*bufLen)]   
        BYTE               buffer[],  
    [out] ULONG32          *bufLen  
);  
```  
  
#### <a name="parameters"></a>参数  
 `address`  
 [in]A`CORDB_ADDRESS`对象，它指定的本机映像偏移量。  
  
 `bufsize`  
 [in]大小，以字节为单位的`buffer`数组。  
  
 `buffer`  
 [out]一个数组，包含由断点替换操作码。  
  
 `bufLen`  
 [out]指向返回中的字节数的指针`buffer`数组。  
  
## <a name="remarks"></a>备注  
 如果公共语言运行时 (CLR) 内的本机映像偏移量，则将忽略断点。 这样，以避免断点设置由调试器时调度带的断点，CLR。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** CorDebug.idl、 CorDebug.h  
  
 **库：** CorGuids.lib  
  
 **.NET framework 版本：** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]
