---
title: Silverlight 的 CreateDebuggingInterfaceFromVersion 函数
ms.date: 03/30/2017
f1_keywords:
- CreateDebuggingInterfaceFromVersion
helpviewer_keywords:
- CreateDebuggingInterfaceFromVersion function
- debugging API [Silverlight]
- Silverlight, debugging
ms.assetid: 35c7a18f-133a-4584-bd25-bb338568b0c6
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 53571268391011cc1dc0ff112d484e1fa140057f
ms.sourcegitcommit: 3d5d33f384eeba41b2dff79d096f47ccc8d8f03d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33407709"
---
# <a name="createdebugginginterfacefromversion-function-for-silverlight"></a>Silverlight 的 CreateDebuggingInterfaceFromVersion 函数
接受从返回的公共语言运行时 (CLR) 版本字符串[CreateVersionStringFromModule 函数](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md)，并返回相应的调试器接口 (通常情况下， [ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md))。  
  
## <a name="syntax"></a>语法  
  
```  
HRESULT CreateDebuggingInterfaceFromVersion (  
    [in]  LPCWSTR      szDebuggeeVersion,  
    [out] IUnknown**   ppCordb,  
);  
```  
  
#### <a name="parameters"></a>参数  
 `szDebuggeeVersion`  
 [in]目标调试对象，返回的 clr 的版本字符串[CreateVersionStringFromModule 函数](../../../../docs/framework/unmanaged-api/debugging/createversionstringfrommodule-function.md)。  
  
 `ppCordb`  
 [out] 指向“COM 对象的指针”的指针 (`IUnknown`)。 此对象强制转换为[ICorDebug](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)对象，然后它返回的状态。  
  
## <a name="return-value"></a>返回值  
 S_OK  
 `ppCordb` 引用有效的对象实现[ICorDebug 接口](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)接口。  
  
 E_INVALIDARG  
 `szDebuggeeVersion` 或 `ppCordb` 为 null。  
  
 CORDBG_E_DEBUG_COMPONENT_MISSING  
 找不到 CLR 调试所需的组件。 这意味着未能在与目标 CoreCLR.dll 相同的目录中找到 mscordbi.dll 或 mscordaccore.dll。  
  
 CORDBG_E_INCOMPATIBLE_PROTOCOL  
 mscordbi.dll 或 mscordaccore.dll 与目标 CoreCLR.dll 版本不一致。  
  
 E_FAIL（或其他 E_ 返回代码）  
 无法返回[ICorDebug 接口](../../../../docs/framework/unmanaged-api/debugging/icordebug-interface.md)。  
  
## <a name="remarks"></a>备注  
 返回的接口提供用于附加到目标进程中的 CLR 和调试 CLR 正在运行的托管代码的功能。  
  
## <a name="requirements"></a>要求  
 **平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。  
  
 **标头：** dbgshim.h  
  
 **库：** dbgshim.dll  
  
 **.NET framework 版本：** 3.5 SP1
