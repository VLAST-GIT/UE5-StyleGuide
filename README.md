# UE5 스타일 가이드 (ver. VLAST)


다음 문서와 예제의 영향을 받아 작성되었습니다.  
[UE4 코딩표준](https://docs.unrealengine.com/4.26/ko/ProductionPipelines/DevelopmentSetup/CodingStandard/)  
[ue5-style-guide](https://github.com/Allar/ue5-style-guide#structure-assettypes)  
[UE 마켓플레이스 가이드라인](https://www.unrealengine.com/ko/marketplace-guidelines?sessionInvalidated=true)  
[UE Recommended Asset Naming Conventions](https://docs.unrealengine.com/4.27/ko/ProductionPipelines/AssetNaming/)  
[LyraStarterGame](https://www.unrealengine.com/marketplace/en-US/product/lyra)  

<br>
<br>

## **목차**
- [**중요한 용어들**]()
  - [맵(map)과 레벨(level)](#맵map과-레벨level)
  - [명명 규칙 종류](#명명-규칙-종류)
  - [변수(Variable)와 프로퍼티(Property)](#변수variable와-프로퍼티property))
    - [프로퍼티(Property)](#프로퍼티-property)
    - [변수(Variable)](#변수-variable)
- [**00. 원칙들**](#00-원칙들)
  - [00.1 당신이 기존에 어떤 스타일을 가지고 있었든, VLAST 소속의 UE 작업자는 모두 이 스타일 가이드를 따라 작업해야 합니다.](#001-당신이-기존에-어떤-스타일을-가지고-있었든-vlast-소속의-ue-작업자는-모두-이-스타일-가이드를-따라-작업해야-합니다)
  - [00.2 프로젝트는 아무리 많은 사람이 참여했다 하더라도, 이 스타일 가이드에 따라 모두 한 사람이 작업한 것처럼 보여야 합니다.](#002-프로젝트는-아무리-많은-사람이-참여했다-하더라도-이-스타일-가이드에-따라-모두-한-사람이-작업한-것처럼-보여야-합니다)
  - [00.3 스타일 가이드를 지키지 않는 팀원을 그대로 내버려두어선 안됩니다.](#003-스타일-가이드를-지키지-않는-팀원을-그대로-내버려두어선-안됩니다)
- [**01. 금지된 사항들**](#01-금지된-사항들)
  - [01.1 금지된 문자](#011-금지된-문자)
- [**02. BaseEngineConfig 설정**]()
  - [02.1 BaseEngine.ini]()
  - [02.2 BaseEditorPerProjectUserSettings.ini]()
- [**1. 에셋 명명 규칙**](#1-에셋-명명-규칙)
  - [1.1 에셋명 기본 형식: `접두사_기본에셋명_세부변형_접미사`](#11-에셋명-기본-형식-접두사_기본에셋명_세부변형_접미사)
    - [1.1 에셋 명명 예](#11의-예시들)
  - [1.2 에셋 접두사 & 접미사 테이블](#12-에셋-접두사--접미사-테이블)
    - [1.2.1 흔히 사용되는 에셋](#121-흔히-사용되는-에셋)
    - [1.2.2 애니메이션 (Animations)](#122-애니메이션-animations)
    - [1.2.3 인공 지능 (Artificial Intelligence)](#123-인공-지능-artificial-intelligence)
    - [1.2.4 블루프린트 (Blueprints)](#124-블루프린트-blueprints)
    - [1.2.5 머티리얼 (Materials)](#125-머티리얼-materials)
    - [1.2.6 텍스처 (Textures)](#126-텍스처-textures)
      - [1.2.6.1 패킹된 텍스처 (Texture Packing)](#1261-패킹된-텍스처-texture-packing)
    - [1.2.7 기타 (Miscellaneous)](#127-기타-miscellaneous)
    - [1.2.8 페이퍼 2D (Paper 2D)](#128-페이퍼-2d-paper-2d)
    - [1.2.9 피직스 (Physics)](#129-피직스-physics)
    - [1.2.10 사운드 (Sounds)](#1210-사운드-sounds)
    - [1.2.11 유저 인터페이스 (User Interface)](#1211-유저-인터페이스-user-interface)
    - [1.2.12 FX](#1212-fx)
    - [1.2.13 미디어 (Media)](#1213-미디어-media)
- [**2. Content 폴더 디렉터리 구조**](#2-content-폴더-디렉터리-구조)
  - [2.0 Content 폴더 디렉터리 구조 예제](#20-content-폴더-디렉터리-구조-예제)
  - [2.1 폴더명 규칙](#21-폴더명-규칙)
    - [2.1.1 항상 파스칼 케이스(PascalCase)를 사용할 것](#211-항상-파스칼-케이스pascalcase를-사용할-것)
    - [2.1.2 공백(스페이스바)을 사용하지 말 것](#212-공백스페이스바을-사용하지-말-것)
    - [2.1.3 영문과 숫자 이외의 문자(특수문자 포함)를 사용하지 말 것](#213-영문과-숫자-이외의-문자특수문자-포함를-사용하지-말-것)
  - [2.2 Use A Top Level Folder For Project Specific Assets](#structure-top-level)
    - [2.2.1 No Global Assets](#2.2.1)
    - [2.2.2 Reduce Migration Conflicts](#2.2.2)
      - [2.2.2e1 Master Material Example](#2.2.2e1)
    - [2.2.3 Samples, Templates, and Marketplace Content Are Risk-Free](#2.2.3)
    - [2.2.4 DLC, Sub-Projects, and Patches Are Easily Maintained](#2.2.4)
  - [2.3 Use Developers Folder For Local Testing](#structure-developers)
  - [2.4 All Map<sup>*</sup> Files Belong In A Folder Called Maps](#structure-maps)
  - [2.5 Use A `Core` Folder For Critical Blueprints And Other Assets](#structure-core)
  - [2.6 Do Not Create Folders Called `Assets` or `AssetTypes`](#structure-assettypes)
    - [2.6.1 Creating a folder named `Assets` is redundant](#2.6.1)
    - [2.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant](#2.6.2)
  - [2.7 Very Large Asset Sets Get Their Own Folder Layout](#structure-large-sets)
  - [2.8 `MaterialLibrary`](#structure-material-library)
  - [2.9 No Empty Folders](#structure-no-empty-folders)
- [**3. 블루프린트 코딩 표준**](#bp)
  - [3.1 Compiling](#bp-compiling)
  - [3.2 Variables](#bp-vars)
    - [3.2.1 Naming](#bp-var-naming)
      - [3.2.1.1 Nouns](#bp-var-naming-nouns)
      - [3.2.1.2 PascalCase](#bp-var-naming-case)
        - [3.2.1.2e Examples](#3.2.1.2e)
      - [3.2.1.3 Boolean `b` Prefix](#bp-var-bool-prefix)
      - [3.2.1.4 Boolean Names](#bp-var-bool-names)
        - [3.2.1.4.1 General And Independent State Information](#3.2.1.4.1)
        - [3.2.1.4.2 Complex States](#3.2.1.4.2)
      - [3.2.1.5 Considered Context](#bp-vars-naming-context)
        - [3.2.1.5e Examples](#3.2.1.5e)
      - [3.2.1.6 Do _Not_ Include Atomic Type Names](#bp-vars-naming-atomic)
      - [3.2.1.7 Do Include Non-Atomic Type Names](#bp-vars-naming-complex)
      - [3.2.1.8 Arrays](#bp-vars-naming-arrays)
    - [3.2.2 Editable Variables](#bp-vars-editable)
      - [3.2.2.1 Tooltips](#bp-vars-editable-tooltips)
      - [3.2.2.2 Slider And Value Ranges](#bp-vars-editable-ranges)
    - [3.2.3 Categories](#bp-vars-categories)
    - [3.2.4 Variable Access Level](#bp-vars-access)
      - [3.2.4.1 Private Variables](#bp-vars-access-private)
    - [3.2.5 Advanced Display](#bp-vars-advanced)
    - [3.2.6 Transient Variables](#bp-vars-transient)
    - [3.2.8 Config Variables](#bp-vars-config)
  - [3.3 Functions, Events, and Event Dispatchers](#bp-functions)
    - [3.3.1 Function Naming](#bp-funcs-naming)
    - [3.3.1.1 All Functions Should Be Verbs](#bp-funcs-naming-verbs)
    - [3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`](#bp-funcs-naming-onrep)
    - [3.3.1.3 Info Functions Returning Bool Should Ask Questions](#bp-funcs-naming-bool)
    - [3.3.1.4 Event Handlers and Dispatchers Should Start With `On`](#bp-funcs-naming-eventhandlers)
    - [3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target](#bp-funcs-naming-rpcs)
    - [3.3.2 All Functions Must Have Return Nodes](#bp-funcs-return)
    - [3.3.3 No Function Should Have More Than 50 Nodes](#bp-graphs-funcs-node-limit)
    - [3.3.4 All Public Functions Should Have A Description](#bp-graphs-funcs-description)
    - [3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name](#bp-graphs-funcs-plugin-category)
  - [3.4 Blueprint Graphs](#bp-graphs)
    - [3.4.1 No Spaghetti](#bp-graphs-spaghetti)
    - [3.4.2 Align Wires Not Nodes](#bp-graphs-align-wires)
    - [3.4.3 White Exec Lines Are Top Priority](#bp-graphs-exec-first-class)
    - [3.4.4 Graphs Should Be Reasonably Commented](#bp-graphs-block-comments)
    - [3.4.5 Graphs Should Handle Casting Errors Where Appropriate](#bp-graphs-cast-error-handling)
    - [3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes](#bp-graphs-dangling-nodes)
- [4. Static Meshes](#4)
  - [4.1 Static Mesh UVs](#s-uvs)
    - [4.1.1 All Meshes Must Have UVs](#s-uvs-no-missing)
    - [4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps](#s-uvs-no-overlapping)
  - [4.2 LODs Should Be Set Up Correctly](#s-lods)
  - [4.3 Modular Socketless Assets Should Snap To The Grid Cleanly](#s-modular-snapping)
  - [4.4 All Meshes Must Have Collision](#s-collision)
  - [4.5 All Meshes Should Be Scaled Correctly](#s-scaled)
- [5. Niagara](#Niagara)
  - [5.1 No Spaces, Ever](#ng-rules)
- [6. Levels / Maps](#levels)
  - [6.1 No Errors Or Warnings](#levels-no-errors-or-warnings)
  - [6.2 Lighting Should Be Built](#levels-lighting-should-be-built)
  - [6.3 No Player Visible Z Fighting](#levels-no-visible-z-fighting)
  - [6.4 Marketplace Specific Rules](#levels-mp-rules)
    - [6.4.1 Overview Level](#levels-mp-rules-overview)
    - [6.4.2 Demo Level](#levels-mp-rules-demo)
- [7. Textures](#textures)
  - [7.1 Dimensions Are Powers of 2](#textures-dimensions)
  - [7.2 Texture Density Should Be Uniform](#textures-density)
  - [7.3 Textures Should Be No Bigger than 8192](#textures-max-size)
  - [7.4 Textures Should Be Grouped Correctly](#textures-group)





<br>
<br>

## **중요한 용어들**


### 맵(map)과 레벨(level)

맵(map)은 일반적으로 게임플레이의 월드가 되는 레벨(level)을 의미합니다.  

<br>

### 명명 규칙 종류
 #### 파스칼 케이스 (PascalCase)  
 - 띄어쓰기를 모두 붙여서 표현합니다. 즉, 공백이 없습니다.  
 - 각 단어의 첫 글자는 대문자가 됩니다.   
 - 예시는 다음과 같습니다.  
 `DesertEagle`, `StyleGuide`, `ASeriesOfWords`.

 #### 카멜 케이스 (camelCase) 
 - 파스칼 케이스와 비슷하지만 첫 문자는 항상 소문자입니다
 - 예시는 다음과 같습니다.  
 `desertEagle`, `styleGuide`, `aSeriesOfWords`.

 #### 스네이크 케이스 (snake_case)
 - 띄어쓰기를 밑줄(언더바)로 표시합니다.  
 - 일반적으로 모두 소문자로 표시하지만, 경우에 따라 모두 대문자로 표시하기도 합니다.  
 - 예시는 다음과 같습니다.  
 `desert_Eagle`, `style_guide`, `A_SERIES_OF_WORDS`.

<br>

### 변수(Variable)와 프로퍼티(Property)
 일반적인 맥락에서, 변수와 프로퍼티는 서로 혼용이 가능합니다. 만약 동일한 문맥 내에서 두 용어가 혼용되는 경우 정확한 의미는 다음과 같습니다.  

 

 #### 프로퍼티 (Property)
 일반적으로 클래스 내부 멤버로서 정의된 변수를 의미합니다. 예를 들어, `BP_Bomb` 클래스가 변수 `bExploded`를 멤버로 가지고 있다면, `bExploded`는 `BP_Bomb`의 프로퍼티입니다.  
 
 
 
 #### 변수 (Variable)
 일반적으로 함수의 매개변수 또는 함수 내부의 지역변수로 정의된 변수를 의미합니다.  
 



<br>
<br>


## **00. 원칙들**


### **00.1** 당신이 기존에 어떤 스타일을 가지고 있었든, VLAST 소속의 UE 작업자는 모두 이 스타일 가이드를 따라 작업해야 합니다.  

만약 이 스타일 가이드에 변경이 필요하다 생각한다면, 팀에 새로운 스타일을 제시하고 논의하시면 됩니다.  


### **00.2** 프로젝트는 아무리 많은 사람이 참여했다 하더라도, 이 스타일 가이드에 따라 모두 한 사람이 작업한 것처럼 보여야 합니다.

하나의 스타일 가이드를 따라 협업하는 프로젝트는 마치 한 사람이 제작한 것처럼 일관성이 유지됩니다. 이는 작업 과정에서의 모호성을 없애고 다른 팀원의 작업에 대한 불확실한 짐작을 할 필요가 없도록 만들어 줍니다. 그 결과 팀은 더 나은 생산성을 얻게 되며, 유지보수가 쉬워지게 됩니다.


### **00.3** 스타일 가이드를 지키지 않는 팀원을 그대로 내버려두어선 안됩니다.

만약 당신이 스타일 가이드를 지키지 않은 구조, 에셋명, 코드 등을 보게 된다면, 당신은 즉시 그것을 작성한 팀원에게 이를 알리고 스타일 가이드를 지키도록 정정해주어야 합니다.

모든 사람이 같은 스타일 가이드를 지킨다는 것은 팀원 간의 질문과 답변을 더욱 쉽게 해줍니다. 아무렇게나 꼬아놓은 블루프린트를 풀거나 알 수 없는 변수명으로 가려진 머티리얼에 생긴 문제를 해결해주는 걸 좋아하는 사람은 없습니다.

명확한 스타일 가이드가 없는 팀은 협업 능력이 없는 팀입니다.


<br>
<br>

## **01. 금지된 사항들**


### **01.1** 금지된 문자

아래의 문자들은 에셋명, 폴더명, 변수명 등 프로젝트 내 어디에서도 사용되어선 안됩니다.  
* ` ` 공백 (스페이스바)
* `\` 백슬래시 기호
* `#!@$%` 대부분의 특수 기호
* 한글 등 모든 유니코드 문자 (즉, 영문이 아닌 대부분의 문자)


즉, 다음의 문자들만 허용됩니다.
* `A-Z` ABCDEFGHIJKLMNOPQRSTUVWXYZ
* `a-z` abcdefghijklmnopqrstuvwxyz
* `0-9` 0123456789
* `_` 밑줄(언더바)

금지된 문자를 사용하지 않는 것은 모든 데이터의 모든 플랫폼으로의 포팅 호환성을 높여줍니다.


<br>
<br>


## 1. 에셋 명명 규칙

스타일 가이드의 모든 부분이 그렇지만, 에셋 명명 규칙은 반드시 지켜야 합니다.  
명명 규칙에 따라 일관되게 지어진 에셋 이름은 에셋 관리, 검색, 분석, 유지보수를 매우 쉽게 만들어줍니다.

명명 규칙의 큰 틀은 다음과 같이 `_`(밑줄)에 의해 에셋의 종류, 이름 등을 구분합니다.

<br>

### 1.1 에셋명 기본 형식: `접두사_기본에셋명_세부변형_접미사`  

`접두사`와 `접미사`는 에셋 형식에 따라 다음의 [1.2 에셋 접두사 & 접미사 테이블](#12-에셋-접두사--접미사-테이블)에 의해 결정됩니다.

모든 에셋들은 기본이 되는 에셋 이름인 `기본에셋명`을 가져야만 합니다. `기본에셋명`은 그 에셋이 속한 그룹의 문맥에 연관되는 짧고 쉬운 이름일수록 좋습니다. 예를 들어 캐릭터의 이름이 `Nina`라면, 모든 Nina 에셋들의 `기본에셋명`이 `Nina`가 되어야 합니다.

`세부변형`은 기본에셋에서 `파생된 다양한 변형의 이름`을 지칭합니다. 예를 들어 `Nina` 캐릭터 에셋에는 다양한 `스킨 변형`이 있을 수 있습니다. Nina 스켈레탈 메시 중 `캐주얼 스타일`의 스킨이 있다면 에셋명은 SKM_Nina_`Casual` 이 됩니다.  
또다른 예로 `레트로 스타일`의 스킨이 있다면, 에셋명은 SKM_Nina_`Retro` 가 됩니다.  

이 스켈레탈 메시에 사용되는 텍스쳐 에셋명의 좋은 예는 캐주얼 스킨의 경우 `T_Nina_Casual_Top_D`, `T_Nina_Casual_Top_N`, `T_Nina_Casual_Feet_D`, 레트로의 경우 `T_Nina_Retro_Top_D`, `T_Nina_Retro_Bottom_D` 가 좋은 예시가 됩니다.

만약 기본에셋명에서 파생되는 변형이 특정 이름으로 표현하기에는 애매한 눈에 띄는 특징이 없는 경우, 변형 이름을 숫자로 대신할 수 있습니다. 예를 들어 모델러가 다양한 종류의 암석을 디자인했을 때, 그것들의 변형은 SM_Rock_`01`, SM_Rock_`02`, SM_Rock_`03` 같은 형태가 될 수 있습니다. 또는 다음과 같이 특정 변형이름 다음에 변형숫자가 올 수도 있습니다. SM_Rock_Tropical_`01`, SM_Rock_Tropical_`02`


#### 1.1의 예시들

##### 기본에셋명 `Nina`의 `CasualOffice`변형 예

| 에셋 유형                                  | 에셋명                            |
| ----------------------------------------- | -------------------------------- |
| 스켈레탈 메시(Skeletal Mesh) *상의*        | SKM_Nina_Suit_Shirt               |
| 스켈레탈 메시(Skeletal Mesh) *하의*        | SKM_Nina_Suit_Slacks              |
| 머티리얼 (Material) *상의*                 | M_Nina_Suit_Shirt                 |
| 텍스처 (Texture) *Diffuse/Albedo*         | T_Nina_Suit_Shirt_D               |
| 텍스처 (Texture) *Normal*                 | T_Nina_Suit_Shirt_N               |

##### 기본에셋명 `Rock`의 `불특정 변형` 예

| 에셋 유형                                                         | 에셋명                                |
| ---------------------------------------------------------------- | ------------------------------------- |
| 스태틱 메시 (Static Mesh) *변형1*                                 | SM_Rock_01                             |
| 스태틱 메시 (Static Mesh) *변형2*                                 | SM_Rock_02                             |
| 스태틱 메시 (Static Mesh) *변형3*                                 | SM_Rock_03                             |
| 머티리얼 (Material) *변형들의 마스터*                              | M_Rock                                 |
| 머티리얼 인스턴스 (Material Instance) *변형1의 인스턴스*            | MI_Rock_01                            |
| 머티리얼 인스턴스 (Material Instance) *눈쌓인 번형 인스턴스*        | MI_Rock_Snow_01                       |

<br>

### 1.2 에셋 접두사 & 접미사 테이블

[1.1 에셋명 기본 형식](#11-에셋명-기본-형식-접두사_기본에셋명_세부변형_접미사)의 `접두사`, `접미사` 규칙입니다. 


#### 1.2.1 흔히 사용되는 에셋

| 에셋 유형                              | 접두사     | 접미사     | Notes                            |
| ------------------------------------- | ---------- | ---------- | -------------------------------- |
| 레벨                           |            |            | `Maps` 폴더 안에 있어야 한다.      |
| 블루프린트                  | BP_        |            |                                  |
| 머티리얼                    | M_         |            |                                  |
| 머티리얼 인스턴스   | MI_         |            |                                  |
| 스태틱 메시              | SM_        |            |                                  |
| 스켈레탈 메시          | SKM_       |            |                                  |
| 텍스처                       | T_         | _?         | 접미사 디테일은 [텍스처 (Textures)](#126-텍스처-textures) 항목을 봐주세요.    |
| 나이아가라 시스템      | NS_        |            |                                  |
| 위젯 블루프린트      | WBP_       |            |                                  |


#### 1.2.2 애니메이션 (Animations)

| 에셋 유형                                      | 접두사     | 접미사     | Notes                            |
| --------------------------------------------- | ---------- | ---------- | -------------------------------- |
| 에임 오프셋                        | AO_        |            |                                  |
| 에임 오프셋 1D                  | AO_        |            |                                  |
| 애니메이션 블루프린트      | ABP_       |            |                                  |
| 애니메이션 컴포짓          | AC_        |            |                                  |
| 애니메이션 몽타주            | AM_        |            |                                  |
| 애니메이션 시퀀스           | A_         |            |                                  |
| 블렌드 스페이스                    | BS_        |            |                                  |
| 블렌드 스페이스 1D              | BS_        |            |                                  |
| 레벨 시퀀스                    | LS_         |            |                                  |
| 페이퍼 플립북 *Paper Flipbook*                 | PFB_        |            |                                  |
| 컨트롤 릭 *Control Rig*                        | CR_         |            |                                  |
| IK 릭 *IK Rig*                                 | IK_        |            |                                  |
| IK 리타기터 *IK Retargeter*                     | RTG_       |            |                                  |
| 스켈레탈 메시 *Skeletal Mesh*                   | SKM_       |            |                                  |
| 스켈레톤 *Skeleton*                             | SKEL_      |            |                                  |


#### 1.2.3 인공 지능 (Artificial Intelligence)

| 에셋 유형                | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| AI Controller           | AIC_       |            |                                  |
| Behavior Tree           | BT_        |            |                                  |
| Blackboard              | BB_        |            |                                  |
| Decorator               | BTDecorator_ |          |                                  |
| Service                 | BTService_ |            |                                  |
| Task                    | BTTask_    |            |                                  |
| Environment Query       | EQS_       |            |                                  |
| EnvQueryContext         | EQS_       | Context    |                                  |


#### 1.2.4 블루프린트 (Blueprints)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 블루프린트                | BP_        |            |                                  |
| 블루프린트 컴포넌트      | BPC_        |            |         |
| 블루프린트 함수 라이브러리  | BPFL_   |            |                                  |
| 블루프린트 인터페이스      | BPI_       |            |                                  |
| 블루프린트 매크로 라이브러리  | BPML_      |            | 가능한 한 사용하지 않는다. |
| 열거형 *Enumeration*             | E          |            | 접두사 후 밑줄 없음. eg. `ECharacterState`                   |
| 구조체 *Structure*               | S     |            | 접두사 후 밑줄 없음.                  |
| 위젯 블루프린트         | WBP_       |            |                                  |
| 게임플레이 어빌리티         | GA_       |            |                                  |


#### 1.2.5 머티리얼 (Materials)

| 에셋 유형                    | 접두사     | 접미사     | Notes                            |
| ----------------------------- | ---------- | ---------- | -------------------------------- |
| 머티리얼                       | M_         |            |                                  |
| 머티리얼 (포스트 프로세스)       | M_PP_        |            |                                  |
| 머티리얼 (데칼)       | M_Decal_        |            |                                  |
| 머티리얼 인스턴스              | MI_        |            |                                  |
| 머티리얼 인스턴스 (포스트 프로세스)             | MI_PP_        |            |                                  |
| 머티리얼 인스턴스 (데칼)             | MI_Decal_        |            |                                  |
| 머티리얼 함수              | MF_        |            |                                  |
| 머티리얼 파라미터 컬렉션  | MPC_       |            |                                  |
| 서브서피스 프로파일 *Subsurface Profile*            | SSP_        |            |                                  |
| 피직스 머티리얼             | PM_        |            |                                  |


#### 1.2.6 텍스처 (Textures)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 텍스처                  | T_         |            |                                  |
| - Diffuse/Albedo/Base Color| T_ | _D      |                                  |
| - Normal        | T_         | _N         |                                  |
| - Roughness     | T_         | _R         |                                  |
| - Alpha/Opacity | T_         | _A         |                                  |
| - Ambient Occlusion | T_     | _O         |                                  |
| - Bump          | T_         | _B         |                                  |
| - Emissive      | T_         | _E         |                                  |
| - Mask          | T_         | _M         |                                  |
| - Specular      | T_         | _S         |                                  |
| - Metallic      | T_         | _M         |                                  |
| - RGB채널에 패킹된 텍스처        | T_         | _*         | 아래의 [패킹된 텍스처 (Texture Packing)](#1261-패킹된-텍스처-texture-packing)를 참고해주세요. |
| 텍스처 큐브 *Texture Cube*            | TC_        |            |                                  |
| 미디어 텍스처 *Media Texture*           | MT_        |            |                                  |
| 렌더 타깃 *Render Target*           | RT_        |            |                                  |
| 큐브 렌더 타깃       | RTC_       |            |                                  |


##### 1.2.6.1 패킹된 텍스처 (Texture Packing)

`Roughness`, `Ambient Occlusion`, `Metallic` 등 여러 개의 맵을 RGB채널에 각각 할당해 하나의 텍스처로 패킹하는 것이 일반적입니다. 패킹된 텍스처의 접미사는 RGB 채널에 할당된 맵의 순서를 따릅니다.  
예를 들어, `Emissive`, `Roughness`, `Ambient Occlusion` 맵을 각각 `Red`, `Green`, `Blue` 채널에 할당한 경우, `접미사`는 RGB에 할당된 순서에 따라 `_ERO`가 됩니다.

> RGBA 4채널 패킹은 추천하지 않습니다.  
> 기본 텍스처 압축 포맷이 알파채널 압축을 지원하지 않아, 4채널 압축을 위한 추가적인 연산이 필요해지기 때문입니다. 


#### 1.2.7 기타 (Miscellaneous)

| 에셋 유형                 | 접두사     | 접미사     | Notes                            |
| -------------------------- | ---------- | ---------- | -------------------------------- |
| 데이터 에셋                 | DA_         |            |  |
| 데이터 테이블                | DT_        |            |                                  |
| 플롯 커브                | CV_     | _Float     |                                  |
| 벡터 커브               | CV_     | _Vector    |                                  |
| 컬러 커브                | CV_     | _Color     |                                  |
| 커브 테이블                | CV_     | _Table     |                                  |
| 벡터 필드        | VF_        |            |                                  |
| HLOD 레이어        | HLODLayer_        |            |                                  |
| 그룸 *Groom*       | Groom_        |            |                                  |


#### 1.2.8 페이퍼 2D (Paper 2D)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Paper Flipbook          | PFB_       |            |                                  |
| Sprite                  | SPR_       |            |                                  |
| Sprite Atlas Group      | SPRG_      |            |                                  |
| Tile Map                | TM_        |            |                                  |
| Tile Set                | TS_        |            |                                  |


#### 1.2.9 피직스 (Physics)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 피직스 머티리얼       | PM_        |            |                                  |
| 피직스 에셋           | PA_      |            |                                  |
| 지오메트리 컬렉션       | GC_        |            |                                  |
| 지오메트리 컬렉션 캐시           | GC_      | _Cache           |                                  |
| 카오스 솔버       | Solver_        |            |                                  |
| 카오스 캐시 컬렉션           | Chaos_      | _Cache           |                                  |


#### 1.2.10 사운드 (Sounds)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Dialogue Voice          | DV_        |            |                                  |
| Dialogue Wave           | DW_        |            |                                  |
| Reverb Effect           | Reverb_    |            |                                  |
| Sound Attenuation       | ATT_       |            |                                  |
| Sound Class             |            |            | No prefix/suffix. Should be put in a folder called SoundClasses |
| Sound Concurrency       |            | _SC        | Should be named after a SoundClass |
| Sound Cue               | A_         | _Cue       |                                  |
| Sound Mix               | Mix_       |            |                                  |
| Sound Wave              | A_         |            |                                  |
| 메타 사운드              | MS_         |            |                                  |
| 메타 사운드 소스              | MSS_         |            |                                  |
| 컨트롤 버스              | CB_         |            |                                  |
| 컨트롤 버스 믹스              | CBM_         |            |                                  |


#### 1.2.11 유저 인터페이스 (User Interface)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| Font                    | Font_      |            |                                  |
| 위젯 블루프린트          | WBP_       |            |                                  |


#### 1.2.12 FX

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| 나이아가라 시스템          | NS_        |            |                                  |
| 나이아가라 모듈          | NM_        |            |                                  |
| Niagara Dynamic Input Script          | NM_        |            |                                  |
| 나이아가라 이미터          | NE_        |            |                                  |
| 나이아가라 이펙트 타입          | EffectType_        |            |                                  |
| 나이아가라 파라미터 컬렉션          | NPC_        |            |                                  |
| - 인스턴스          | NPCI_        |            |                                  |


#### 1.2.13 미디어 (Media)

| 에셋 유형              | 접두사     | 접미사     | Notes                            |
| ----------------------- | ---------- | ---------- | -------------------------------- |
| File Media Source          | MS_File_        |            |                                  |
| Img Media Source           | MS_Img_        |            |                                  |
| Stream Media Source        | MS_Stream_        |            |                                  |
| Media Player               | MP_        |            |                                  |
| Media Texture              | MT_        |            |                                  |


**[⬆ Back to Top](#목차)**

<br>
<br>

## 2. Content 폴더 디렉터리 구조

에셋 명명 규칙과 마찬가지로, 프로젝트 디렉터리 구조 스타일 역시 반드시 지켜주셔야 합니다.  
에셋 이름과 Content 디렉터리 구조는 서로 연관이 깊으며, 둘 중 하나를 위반한다면 불필요한 혼란이 생기게 됩니다.  

<br>

### 2.0 Content 폴더 디렉터리 구조 예제

프로젝트 이름 `NinaVirtual`의 `Content`폴더 디렉터리 구조 예제
<pre>
|-- Content
    |-- <a href="#2.2">GenericShooter</a>
        |-- 3D_Assets
        |   |-- Industrial
        |   |   |-- Ambient
        |   |   |-- Machinery
        |   |   |-- Pipes
        |   |-- Nature
        |   |   |-- Ambient
        |   |   |-- Foliage
        |   |   |-- Rocks
        |   |   |-- Trees
        |   |-- Office
        |-- Characters
        |   |-- Bob
        |   |-- Common
        |   |   |-- <a href="#2.7">Animations</a>
        |   |   |-- Audio
        |   |-- Jack
        |   |-- Steve
        |   |-- <a href="#2.1.3">Zoe</a>
        |-- <a href="#2.5">Core</a>
        |   |-- Characters
        |   |-- Engine
        |   |-- <a href="#2.1.2">GameModes</a>
        |   |-- Interactables
        |   |-- Pickups
        |   |-- Weapons
        |-- Effects
        |   |-- Electrical
        |   |-- Fire
        |   |-- Weather
        |-- <a href="#2.4">Maps</a>
        |   |-- Campaign1
        |   |-- Campaign2
        |-- <a href="#2.8">MaterialLibrary</a>
        |   |-- Debug
        |   |-- Metal
        |   |-- Paint
        |   |-- Utility
        |   |-- Weathering
        |-- Placeables
        |   |-- Pickups
        |-- Weapons
            |-- Common
            |-- Pistols
            |   |-- DesertEagle
            |   |-- RocketPistol
            |-- Rifles
</pre>

이러한 구조를 사용하는 이유는 밑의 항목들에서 다룹니다.

<br>

### 2.1 폴더명 규칙

Content 폴더 내의 모든 폴더 이름에 적용되는 공통 규칙들입니다.


#### 2.1.1 항상 파스칼 케이스(PascalCase)를 사용할 것

파스칼 케이스는 첫 문자가 대문자로 시작하며, 각 단어의 시작을 대문자로 구분합니다.
`GameModes`, `DesertEagle` 등이 그 예입니다. 자세한 설명은 [파스칼 케이스(PascalCase)](#파스칼-케이스-pascalcase)를 참고해주세요.

> Maya 작업자의 경우 Maya 내에서는 [카멜 케이스(camelCase)](#카멜-케이스-camelcase)가 표준 스타일인 경우가 많아 이 스타일을 그대로 언리얼 엔진에 적용하시는 경우가 많습니다.  
> 언리얼 엔진에서는 `파스칼 케이스`가 표준임을 유념해주세요.

#### 2.1.2 공백(스페이스바)을 사용하지 말 것

[금지된 문자](#011-금지된-문자)에 따라 폴더 이름에 ` `공백을 사용해선 안됩니다.

#### 2.1.3 영문과 숫자 이외의 문자(특수문자 포함)를 사용하지 말 것

폴더 이름에 허용되는 문자는 `A-Z`, `a-z`, `0-9` 뿐입니다. [금지된 문자](#011-금지된-문자)의 허용된 문자 항목을 참고해주세요.

<br>

### 2.2 최상위 폴더 규칙

프로젝트의 모든 에셋은 프로젝트 이름을 딴 최상위 폴더 내에 위치해야 합니다. 예를 들어, 프로젝트 이름이 `NinaVirtual`이라면 `NinaVirtual` 프로젝트를 위해 생성된 모든 에셋은 `Content\NinaVirtual\` 내에 위치해야 합니다. 만약 프로젝트 이름이 너무 길거나 프로젝트 이름을 그대로 최상위 폴더명으로 따기에 부적합하다 느낄 경우, 적합한 이름으로 변경할 수 있습니다. 

프로젝트 내의 모든 에셋이 프로젝트의 최상위 폴더에 위치해야하는 것은 아닙니다. 다른 프로젝트에서 이주해오거나 프로젝트에 추가한 마켓플레이스 콘텐츠 등이 있을 경우 이주해온 프로젝트의 에셋들도 `최상위 폴더 규칙`에 따라 각자의 최상위 폴더를 가질 것이므로, 한 프로젝트는 다수의 최상위 폴더를 가질 수 있습니다. 자세한 내용은 [다음](#223-최상위-폴더-규칙을-준수하는-샘플-템플릿-마켓플레이스-콘텐츠는-폴더-구조를-수정하지-않습니다)을 확인해주세요.

> `Developers` 폴더는 프로젝트에 종속된 폴더가 아니므로, 프로젝트별로 구분되지 않습니다. 자세한 내용은 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 항목을 참고해주세요.


#### 2.2.1 최상위 폴더 바깥에 에셋을 두어선 안됩니다. 

에셋이 프로젝트의 최상위 폴더 바깥에 위치하는 것은 허용되지 않습니다. 구체적인 예시는 다음과 같습니다.  
프로젝트 `NinaVirtual` 내의 `T_Rock` 에셋이 최상위 폴더 외의 경로에 잘못 위치한 예시들:  
> `Content\T_Rock.uasset`  
> `Content\Textures\T_Rock.uasset`  
> `Content\Temp\T_Rock.uasset`  
> `Content\Test\T_Rock.uasset`  

최상위 폴더 바깥에 위치한 에셋은 팀원들에게 정리할 필요가 없는 에셋이라는 암시를 주게 되며, 이러한 경로의 존재는 에셋을 정리하지 않는 나쁜 습관을 조장하여 올바른 스타일을 따르는 것을 매우 어렵게 만듭니다.  

최상위 폴더 바깥에 에셋이 위치할 경우 그래야만 하는 명확한 목적이 있어야 합니다. 만약 실험적인 목적을 위한 로컬 테스트 에셋이라면 [Developers 폴더](#23-로컬-테스트는-developers-폴더-내에서-해야합니다) 내에 위치해야 합니다.


#### 2.2.2 최상위 폴더 규칙은 이주 충돌을 감소시켜줍니다.

여러 프로젝트에서 작업이 이루어지면서 다른 모든 프로젝트에 유용하게 사용될 에셋이 있는 경우, 한 프로젝트에서 다른 프로젝트로 에셋 그룹을 `이주(Migrate)`하는 것이 일반적입니다. 콘텐츠 브라우저의 이주 기능을 사용하여 에셋을 다른 프로젝트로 복사하는 경우, 에디터의 종속성 검사에 의해 이와 관련된 에셋 일체가 함께 복사됩니다. 

두 프로젝트 사이에 `최상위 폴더 규칙`이 제대로 지켜지지 않는 경우, 에셋의 이주는 쉽게 문제를 일으키게 됩니다. 구체적인 충돌 예시는 다음과 같습니다. 

##### 2.2.2.1 마스터 머티리얼 이주 충돌 예시

`ProjectA`에서 마스터 머티리얼을 만들었고, 이 머티리얼이 `ProjectB`에도 유용하다 판단해 이주하는 상황을 가정합니다. 만약 프로젝트가 최상위 폴더 규칙을 지키지 않는 경우, 마스터 머티리얼은 `Content\MaterialLibrary\M_Master`와 같은 경로에 위치할 확률이 높아집니다.

문제는 `ProjectB`도 최상위 경로 규칙을 지키지 않으며 동일한 경로에 이미 자체적인 마스터 머티리얼이 있을 경우 발생합니다. `ProjectB`의 아티스트들은 지시받은 대로 `Content\MaterialLibrary\M_Mater`의 인스턴스를 생성해 여러 에셋에 이미 이를 적용해두었습니다. 이 상태에서 `ProjectA`의 `M_Master`가 이주되면 기존의 `M_Master`를 덮어씌우며 의도치 않게 기존의 모든 에셋의 룩을 변경하는 결과가 발생하게 됩니다.

이러한 충돌 문제는 이주를 실행하는 당사자가 아티스트라면 미리 예측하기 어려우며, 충돌이 발생한 후에도 문제가 발생한 이유를 쉽게 발견하지 못할 수 있습니다. 스태틱 메시를 이주하는 아티스트는 종속성에 의해 `Content\MaterialLibrary\M_Mater` 에셋이 함께 이주되는 것을 미리 파악하지 못할 수 있으며, 일반적으로 아티스트는 마스터 머티리얼 개발에 익숙한 사람이 아닐 가능성이 높기 때문에 잘못된 덮어씌움으로 기존 에셋에도 문제가 발생했다는 사실을 파악하지 못할 수 있습니다. 

이처럼 최상위 폴더 규칙이 지켜지지 않은 두 프로젝트 사이의 이주는 기존 에셋과의 충돌을 일으킬 확률이 매우 높아집니다. 만일 두 프로젝트가 모두 최상위 폴더 규칙을 지키고 있었다면, `ProjectB`로의 이주 결과는 다음과 같이 되며 충돌을 피할 수 있습니다. 
<pre>
|-- Content
    |-- ProjectA
        |-- MaterialLibrary
        |   |-- M_Master.uasset
    |-- ProjectB
        |-- MaterialLibrary
        |   |-- M_Master.uasset
</pre>


이는 에픽이 마켓플레이스 가이드라인에 동일한 규칙을 적용하는 이유입니다.

#### 2.2.3 최상위 폴더 규칙을 준수하는 샘플, 템플릿, 마켓플레이스 콘텐츠는 폴더 구조를 수정하지 않습니다.

[2.2.2](#222-최상위-폴더-규칙은-이주-충돌을-감소시켜줍니다)의 예를 보듯, 마켓플레이스 콘텐츠, 템플릿 등은 최상위 폴더 규칙을 준수하기 때문에 이러한 에셋의 추가는 프로젝트에 방해가 되지 않습니다.

하지만 마켓플레이스 콘텐츠가 언제나 최상위 폴더 규칙을 준수한다고 신뢰할 수는 없습니다. 마켓플레이스 콘텐츠를 본 프로젝트에 추가하기 전 반드시 테스트 프로젝트에 먼저 추가해본 뒤, 최상위 폴더 규칙을 추가하는 경우에만 본 프로젝트로 이주합니다.

최상위 폴더 규칙을 준수하는 패키지를 올바르게 프로젝트에 추가한 뒤에는 이주된 상태 그대로 별도의 최상위 폴더에 둡니다. 추가한 패키지의 폴더 구조를 변경하거나 기존 프로젝트 최상위 폴더로의 병합은 해당 패키지가 업데이트되거나 패키지에서 추가로 이주할 에셋이 생길 경우 중복된 에셋을 만들거나 이주 충돌이 발생할 확률이 높아지게 됩니다. 이주해온 패키지에 일부 변형을 주고 싶은 경우, `Content\이주 패키지의 최상위폴더\Modified` 폴더를 만들어 패키지에서 변경된 사항은 `Modified` 폴더에 모아 추가 이주로 인한 충돌 가능성을 줄입니다.

추가한 패키지의 최상위 폴더 구조를 변경하는 경우는 해당 패키지를 프로젝트에 완전히 병합하려는 경우에 한합니다.


#### 2.2.4 다른 프로젝트로 자주 이주될 수 있는 에셋 그룹은 별도의 최상위 폴더를 가져야 합니다.

If your project plans to release DLC or has multiple sub-projects associated with it that may either be migrated out or simply not cooked in a build, assets relating to these projects should have their own separate top level content folder. This make cooking DLC separate from main project content far easier. Sub-projects can also be migrated in and out with minimal effort. If you need to change a material of an asset or add some very specific asset override behavior in a patch, you can easily put these changes in a patch folder and work safely without the chance of breaking the core project.

<br>

### 2.3 로컬 테스트는 `Developers` 폴더 내에서 해야합니다.

During a project's development, it is very common for team members to have a sort of 'sandbox' where they can experiment freely without risking the core project. Because this work may be ongoing, these team members may wish to put their assets on a project's source control server. Not all teams require use of Developer folders, but ones that do use them often run into a common problem with assets submitted to source control.

It is very easy for a team member to accidentally use assets that are not ready for use, which will cause issues once those assets are removed. For example, an artist may be iterating on a modular set of static meshes and still working on getting their sizing and grid snapping correct. If a world builder sees these assets in the main project folder, they might use them all over a level not knowing they could be subject to incredible change and/or removal. This causes massive amounts of re-working for everyone on the team to resolve.

If these modular assets were placed in a Developer folder, the world builder should never have had a reason to use them and the whole issue would never happen. The Content Browser has specific View Options that will hide Developer folders (they are hidden by default) making it impossible to accidentally use Developer assets under normal use.

Once the assets are ready for use, an artist simply has to move the assets into the project specific folder and fix up redirectors. This is essentially 'promoting' the assets from experimental to production.

<br>

### 2.4 모든 레벨 에셋은 `Maps` 폴더 내에 위치해야 합니다.

Map files are incredibly special and it is common for every project to have its own map naming system, especially if they work with sub-levels or streaming levels. No matter what system of map organization is in place for the specific project, all levels should belong in `/Content/Project/Maps`.

Being able to tell someone to open a specific map without having to explain where it is is a great time saver and general 'quality of life' improvement. It is common for levels to be within sub-folders of `Maps`, such as `Maps/Campaign1/` or `Maps/Arenas`, but the most important thing here is that they all exist within `/Content/Project/Maps`.

This also simplifies the job of cooking for engineers. Wrangling levels for a build process can be extremely frustrating if they have to dig through arbitrary folders for them. If a team's maps are all in one place, it is much harder to accidentally not cook a map in a build. It also simplifies lighting build scripts as well as QA processes.

<br>

### 2.5 프로젝트에 핵심적인 블루프린트 및 기타 에셋은 `Core` 폴더 내에 위치합니다.

Use `/Content/Project/Core` folder for assets that are absolutely fundamental to a project's workings. For example, base `GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`, and related Blueprints should live here.

This creates a very clear "don't touch these" message for other team members. Non-engineers should have very little reason to enter the `Core` folder. Following good code structure style, designers should be making their gameplay tweaks in child classes that expose functionality. World builders should be using prefab Blueprints in designated folders instead of potentially abusing base classes.

For example, if your project requires pickups that can be placed in a level, there should exist a base Pickup class in `Core/Pickups` that defines base behavior for a pickup. Specific pickups such as a Health or Ammo should exist in a folder such as `/Content/Project/Placeables/Pickups/`. Game designers can define and tweak pickups in this folder however they please, but they should not touch `Core/Pickups` as they may unintentionally break pickups project-wide.

<br>

### 2.6 Do Not Create Folders Called `Assets` or `AssetTypes`


#### 2.6.1 Creating a folder named `Assets` is redundant

All assets are assets.


#### 2.6.2 Creating a folder named `Meshes`, `Textures`, or `Materials` is redundant

All asset names are named with their asset type in mind. These folders offer only redundant information and the use of these folders can easily be replaced with the robust and easy to use filtering system the Content Browser provides.

Want to view only static mesh in `Environment/Rocks/`? Simply turn on the Static Mesh filter. If all assets are named correctly, they will also be sorted in alphabetical order regardless of prefixes. Want to view both static meshes and skeletal meshes? Simply turn on both filters. This eliminates the need to potentially have to `Control-Click` select two folders in the Content Browser's tree view.

> This also extends the full path name of an asset for very little benefit. The `S_` prefix for a static mesh is only two characters, whereas `Meshes/` is seven characters.

Not doing this also prevents the inevitability of someone putting a static mesh or a texture in a `Materials` folder.

<br>

### 2.7 Very Large Asset Sets Get Their Own Folder Layout

This can be seen as a pseudo-exception to [2.6](#2.6).

There are certain asset types that have a huge volume of related files where each asset has a unique purpose. The two most common are Animation and Audio assets. If you find yourself having 15+ of these assets that belong together, they should be together.

For example, animations that are shared across multiple characters should lay in `Characters/Common/Animations` and may have sub-folders such as `Locomotion` or `Cinematic`.

> This does not apply to assets like textures and materials. It is common for a `Rocks` folder to have a large amount of textures if there are a large amount of rocks, however these textures are generally only related to a few specific rocks and should be named appropriately. Even if these textures are part of a [Material Library](#2.8).

<br>

### 2.8 `MaterialLibrary`

If your project makes use of master materials, layered materials, or any form of reusable materials or textures that do not belong to any subset of assets, these assets should be located in `Content/Project/MaterialLibrary`.

This way all 'global' materials have a place to live and are easily located.

> This also makes it incredibly easy to enforce a 'use material instances only' policy within a project. If all artists and assets should be using material instances, then the only regular material assets that should exist are within this folder. You can easily verify this by searching for base materials in any folder that isn't the `MaterialLibrary`.

The `MaterialLibrary` doesn't have to consist of purely materials. Shared utility textures, material functions, and other things of this nature should be stored here as well within folders that designate their intended purpose. For example, generic noise textures should be located in `MaterialLibrary/Utility`.

Any testing or debug materials should be within `MaterialLibrary/Debug`. This allows debug materials to be easily stripped from a project before shipping and makes it incredibly apparent if production assets are using them if reference errors are shown.

<br>

### 2.9 No Empty Folders

There simply shouldn't be any empty folders. They clutter the content browser.

If you find that the content browser has an empty folder you can't delete, you should perform the following:
1. Be sure you're using source control.
1. Immediately run Fix Up Redirectors on your project.
1. Navigate to the folder on-disk and delete the assets inside.
1. Close the editor.
1. Make sure your source control state is in sync (i.e. if using Perforce, run a Reconcile Offline Work on your content directory)
1. Open the editor. Confirm everything still works as expected. If it doesn't, revert, figure out what went wrong, and try again.
1. Ensure the folder is now gone.
1. Submit changes to source control.

**[⬆ Back to Top](#목차)**

<br>
<br>

## 3. 블루프린트 코딩 표준

This section will focus on Blueprint classes and their internals. When possible, style rules conform to [Epic's Coding Standard](https://docs.unrealengine.com/latest/INT/Programming/Development/CodingStandard).

Remember: Blueprinting badly bears blunders, beware! (Phrase by [KorkuVeren](http://github.com/KorkuVeren))


### 3.1 Compiling

All blueprints should compile with zero warnings and zero errors. You should fix blueprint warnings and errors immediately as they can quickly cascade into very scary unexpected behavior.

Do *not* submit broken blueprints to source control. If you must store them on source control, shelve them instead.

Broken blueprints can cause problems that manifest in other ways, such as broken references, unexpected behavior, cooking failures, and frequent unneeded recompilation. A broken blueprint has the power to break your entire game.

<a name="3.2"></a>
<a name="bp-vars"></a>
### 3.2 Variables

The words `variable` and `property` may be used interchangeably.

<a name="3.2.1"></a>
<a name="bp-var-naming"></a>
#### 3.2.1 Naming

<a name="3.2.1.1"></a>
<a name="bp-var-naming-nouns"></a>
##### 3.2.1.1 Nouns

All non-boolean variable names must be clear, unambiguous, and descriptive nouns.

<a name="3.2.1.2"></a>
<a name="bp-var-naming-case"></a>
##### 3.2.1.2 PascalCase

All non-boolean variables should be in the form of [PascalCase](#terms-cases).

<a name="3.2.1.2e"></a>
###### 3.2.1.2e Examples

* `Score`
* `Kills`
* `TargetPlayer`
* `Range`
* `CrosshairColor`
* `AbilityID`

<a name="3.2.1.3"></a>
<a name="bp-var-bool-prefix"></a>
##### 3.2.1.3 Boolean `b` Prefix

All booleans should be named in PascalCase but prefixed with a lowercase `b`.

Example: Use `bDead` and `bEvil`, **not** `Dead` and `Evil`.

UE4 Blueprint editors know not to include the `b` in user-friendly displays of the variable.

<a name="3.2.1.4"></a>
<a name="bp-var-bool-names"></a>
##### 3.2.1.4 Boolean Names

<a name="3.2.1.4.1"></a>
###### 3.2.1.4.1 General And Independent State Information

All booleans should be named as descriptive adjectives when possible if representing general information. Do not include words that phrase the variable as a question, such as `Is`. This is reserved for functions.

Example: Use `bDead` and `bHostile` **not** `bIsDead` and `bIsHostile`.

Try to not use verbs such as `bRunning`. Verbs tend to lead to complex states.

<a name="3.2.1.4.2"></a>
###### 3.2.1.4.2 Complex States

Do not to use booleans to represent complex and/or dependent states. This makes state adding and removing complex and no longer easily readable. Use an enumeration instead.

Example: When defining a weapon, do **not** use `bReloading` and `bEquipping` if a weapon can't be both reloading and equipping. Define an enumeration named `EWeaponState` and use a variable with this type named `WeaponState` instead. This makes it far easier to add new states to weapons.

Example: Do **not** use `bRunning` if you also need `bWalking` or `bSprinting`. This should be defined as an enumeration with clearly defined state names.

<a name="3.2.1.5"></a>
<a name="bp-vars-naming-context"></a>
##### 3.2.1.5 Considered Context

All variable names must not be redundant with their context as all variable references in Blueprint will always have context.

<a name="3.2.1.5e"></a>
###### 3.2.1.5e Examples

Consider a Blueprint called `BP_PlayerCharacter`.

**Bad**

* `PlayerScore`
* `PlayerKills`
* `MyTargetPlayer`
* `MyCharacterName`
* `CharacterSkills`
* `ChosenCharacterSkin`

All of these variables are named redundantly. It is implied that the variable is representative of the `BP_PlayerCharacter` it belongs to because it is `BP_PlayerCharacter` that is defining these variables.

**Good**

* `Score`
* `Kills`
* `TargetPlayer`
* `Name`
* `Skills`
* `Skin`

<a name="3.2.1.6"></a>
<a name="bp-vars-naming-atomic"></a>
##### 3.2.1.6 Do _Not_ Include Atomic Type Names

Atomic or primitive variables are variables that represent data in their simplest form, such as booleans, integers, floats, and enumerations.

Strings and vectors are considered atomic in terms of style when working with Blueprints, however they are technically not atomic.

> While vectors consist of three floats, vectors are often able to be manipulated as a whole, same with rotators.

> Do _not_ consider Text variables as atomic, they are secretly hiding localization functionality. The atomic type of a string of characters is `String`, not `Text`.

Atomic variables should not have their type name in their name.

Example: Use `Score`, `Kills`, and `Description` **not** `ScoreFloat`, `FloatKills`, `DescriptionString`.

The only exception to this rule is when a variable represents 'a number of' something to be counted _and_ when using a name without a variable type is not easy to read.

Example: A fence generator needs to generate X number of posts. Store X in `NumPosts` or `PostsCount` instead of `Posts` as `Posts` may potentially read as an Array of a variable type named `Post`.

<a name="3.2.1.7"></a>
<a name="bp-vars-naming-complex"></a>
##### 3.2.1.7 Do Include Non-Atomic Type Names

Non-atomic or complex variables are variables that represent data as a collection of atomic variables. Structs, Classes, Interfaces, and primitives with hidden behavior such as `Text` and `Name` all qualify under this rule.

> While an Array of an atomic variable type is a list of variables, Arrays do not change the 'atomicness' of a variable type.

These variables should include their type name while still considering their context.

If a class owns an instance of a complex variable, i.e. if a `BP_PlayerCharacter` owns a `BP_Hat`, it should be stored as the variable type as without any name modifications.

Example: Use `Hat`, `Flag`, and `Ability` **not** `MyHat`, `MyFlag`, and `PlayerAbility`.

If a class does not own the value a complex variable represents, you should use a noun along with the variable type.

Example: If a `BP_Turret` has the ability to target a `BP_PlayerCharacter`, it should store its target as `TargetPlayer` as when in the context of `BP_Turret` it should be clear that it is a reference to another complex variable type that it does not own.


<a name="3.2.1.8"></a>
<a name="bp-vars-naming-arrays"></a>
##### 3.2.1.8 Arrays

Arrays follow the same naming rules as above, but should be named as a plural noun.

Example: Use `Targets`, `Hats`, and `EnemyPlayers`, **not** `TargetList`, `HatArray`, `EnemyPlayerArray`.


<a name="3.2.2"></a>
<a name="bp-vars-editable"></a>
#### 3.2.2 Editable Variables

All variables that are safe to change the value of in order to configure behavior of a blueprint should be marked as `Editable`.

Conversely, all variables that are not safe to change or should not be exposed to designers should _not_ be marked as editable, unless for engineering reasons the variable must be marked as `Expose On Spawn`.

Do not arbitrarily mark variables as `Editable`.

<a name="3.2.2.1"></a>
<a name="bp-vars-editable-tooltips"></a>
##### 3.2.2.1 Tooltips

All `Editable` variables, including those marked editable just so they can be marked as `Expose On Spawn`, should have a description in their `Tooltip` fields that explains how changing this value affects the behavior of the blueprint.

<a name="3.2.2.2"></a>
<a name="bp-vars-editable-ranges"></a>
##### 3.2.2.2 Slider And Value Ranges

All `Editable` variables should make use of slider and value ranges if there is ever a value that a variable should _not_ be set to.

Example: A blueprint that generates fence posts might have an editable variable named `PostsCount` and a value of -1 would not make any sense. Use the range fields to mark 0 as a minimum.

If an editable variable is used in a Construction Script, it should have a reasonable Slider Range defined so that someone can not accidentally assign it a large value that could crash the editor.

A Value Range only needs to be defined if the bounds of a value are known. While a Slider Range prevents accidental large number inputs, an undefined Value Range allows a user to specify a value outside the Slider Range that may be considered 'dangerous' but still valid.

<a name="3.2.3"></a>
<a name="bp-vars-categories"></a>
#### 3.2.3 Categories

If a class has only a small number of variables, categories are not required.

If a class has a moderate amount of variables (5-10), all `Editable` variables should have a non-default category assigned. A common category is `Config`.

If a class has a large amount of variables, all `Editable` variables should be categorized into sub-categories using the category `Config` as the base category. Non-editable variables should be categorized into descriptive categories describing their usage.

> You can define sub-categories by using the pipe character `|`, i.e. `Config | Animations`.

Example: A weapon class set of variables might be organized as:

    |-- Config
    |    |-- Animations
    |    |-- Effects
    |    |-- Audio
    |    |-- Recoil
    |    |-- Timings
    |-- Animations
    |-- State
    |-- Visuals

<a name="3.2.4"></a>
<a name="bp-vars-access"></a>
#### 3.2.4 Variable Access Level

In C++, variables have a concept of access level. Public means any code outside the class can access the variable. Protected means only the class and any child classes can access this variable internally. Private means only this class and no child classes can access this variable.

Blueprints do not have a defined concept of protected access currently.

Treat `Editable` variables as public variables. Treat non-editable variables as protected variables.

<a name="3.2.4.1"></a>
<a name="bp-vars-access-private"></a>
##### 3.2.4.1 Private Variables

Unless it is known that a variable should only be accessed within the class it is defined and never a child class, do not mark variables as private. Until variables are able to be marked `protected`, reserve private for when you absolutely know you want to restrict child class usage.

<a name="3.2.5"></a>
<a name="bp-vars-advanced"></a>
#### 3.2.5 Advanced Display

If a variable should be editable but often untouched, mark it as `Advanced Display`. This makes the variable hidden unless the advanced display arrow is clicked.

To find the `Advanced Display` option, it is listed as an advanced displayed variable in the variable details list.

<a name="3.2.6"></a>
<a name="bp-vars-transient"></a>
#### 3.2.6 Transient Variables

Transient variables are variables that do not need to have their value saved and loaded and have an initial value of zero or null. This is useful for references to other objects and actors who's value isn't known until run-time. This prevents the editor from ever saving a reference to it, and speeds up saving and loading of the blueprint class.

Because of this, all transient variables should always be initialized as zero or null. To do otherwise would result in hard to debug errors.

<a name="3.2.7"></a>
<a name="bp-vars-config"></a>
#### 3.2.8 Config Variables

Do not use the `Config Variable` flag. This makes it harder for designers to control blueprint behavior. Config variables should only be used in C++ for rarely changed variables. Think of them as `Advanced Advanced Display` variables.

<a name="3.3"></a>
<a name="bp-functions"></a>
### 3.3 Functions, Events, and Event Dispatchers

This section describes how you should author functions, events, and event dispatchers. Everything that applies to functions also applies to events, unless otherwise noted.

<a name="3.3.1"></a>
<a name="bp-funcs-naming"></a>
#### 3.3.1 Function Naming

The naming of functions, events, and event dispatchers is critically important. Based on the name alone, certain assumptions can be made about functions. For example:

* Is it a pure function?
* Is it fetching state information?
* Is it a handler?
* Is it an RPC?
* What is its purpose?

These questions and more can all be answered when functions are named appropriately.

<a name="3.3.1.1"></a>
<a name="bp-funcs-naming-verbs"></a>
#### 3.3.1.1 All Functions Should Be Verbs

All functions and events perform some form of action, whether its getting info, calculating data, or causing something to explode. Therefore, all functions should all start with verbs. They should be worded in the present tense whenever possible. They should also have some context as to what they are doing.

`OnRep` functions, event handlers, and event dispatchers are an exception to this rule.

Good examples:

* `Fire` - Good example if in a Character / Weapon class, as it has context. Bad if in a Barrel / Grass / any ambiguous class.
* `Jump` - Good example if in a Character class, otherwise, needs context.
* `Explode`
* `ReceiveMessage`
* `SortPlayerArray`
* `GetArmOffset`
* `GetCoordinates`
* `UpdateTransforms`
* `EnableBigHeadMode`
* `IsEnemy` - ["Is" is a verb.](http://writingexplained.org/is-is-a-verb)

Bad examples:

* `Dead` - Is Dead? Will deaden?
* `Rock`
* `ProcessData` - Ambiguous, these words mean nothing.
* `PlayerState` - Nouns are ambiguous.
* `Color` - Verb with no context, or ambiguous noun.

<a name="3.3.1.2"></a>
<a name="bp-funcs-naming-onrep"></a>
#### 3.3.1.2 Property RepNotify Functions Always `OnRep_Variable`

All functions for replicated with notification variables should have the form `OnRep_Variable`. This is forced by the Blueprint editor. If you are writing a C++ `OnRep` function however, it should also follow this convention when exposing it to Blueprints.

<a name="3.3.1.3"></a>
<a name="bp-funcs-naming-bool"></a>
#### 3.3.1.3 Info Functions Returning Bool Should Ask Questions

When writing a function that does not change the state of or modify any object and is purely for getting information, state, or computing a yes/no value, it should ask a question. This should also follow [the verb rule](#bp-funcs-naming-verbs).

This is extremely important as if a question is not asked, it may be assumed that the function performs an action and is returning whether that action succeeded.

Good examples:

* `IsDead`
* `IsOnFire`
* `IsAlive`
* `IsSpeaking`
* `IsHavingAnExistentialCrisis`
* `IsVisible`
* `HasWeapon` - ["Has" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)
* `WasCharging` - ["Was" is past-tense of "be".](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html) Use "was" when referring to 'previous frame' or 'previous state'.
* `CanReload` - ["Can" is a verb.](http://grammar.yourdictionary.com/parts-of-speech/verbs/Helping-Verbs.html)

Bad examples:

* `Fire` - Is on fire? Will fire? Do fire?
* `OnFire` - Can be confused with event dispatcher for firing.
* `Dead` - Is dead? Will deaden?
* `Visibility` - Is visible? Set visibility? A description of flying conditions?

<a name="3.3.1.4"></a>
<a name="bp-funcs-naming-eventhandlers"></a>
#### 3.3.1.4 Event Handlers and Dispatchers Should Start With `On`

Any function that handles an event or dispatches an event should start with `On` and continue to follow [the verb rule](#bp-funcs-naming-verbs). The verb may move to the end however if past-tense reads better.

[Collocations](http://dictionary.cambridge.org/us/grammar/british-grammar/about-words-clauses-and-sentences/collocation) of the word `On` are exempt from following the verb rule.

`Handle` is not allowed. It is 'Unreal' to use `On` instead of `Handle`, while other frameworks may prefer to use `Handle` instead of `On`.

Good examples:

* `OnDeath` - Common collocation in games
* `OnPickup`
* `OnReceiveMessage`
* `OnMessageRecieved`
* `OnTargetChanged`
* `OnClick`
* `OnLeave`

Bad examples:

* `OnData`
* `OnTarget`
* `HandleMessage`
* `HandleDeath`

<a name="3.3.1.5"></a>
<a name="bp-funcs-naming-rpcs"></a>
#### 3.3.1.5 Remote Procedure Calls Should Be Prefixed With Target

Any time an RPC is created, it should be prefixed with either `Server`, `Client`, or `Multicast`. No exceptions.

After the prefix, follow all other rules regarding function naming.

Good examples:

* `ServerFireWeapon`
* `ClientNotifyDeath`
* `MulticastSpawnTracerEffect`

Bad examples:

* `FireWeapon` - Does not indicate its an RPC of some kind.
* `ServerClientBroadcast` - Confusing.
* `AllNotifyDeath` - Use `Multicast`, never `All`.
* `ClientWeapon` - No verb, ambiguous.


<a name="3.3.2"></a>
<a name="bp-funcs-return"></a>
#### 3.3.2 All Functions Must Have Return Nodes

All functions must have return nodes, no exceptions.

Return nodes explicitly note that a function has finished its execution. In a world where blueprints can be filled with `Sequence`, `ForLoopWithBreak`, and backwards reroute nodes, explicit execution flow is important for readability, maintenance, and easier debugging.

The Blueprint compiler is able to follow the flow of execution and will warn you if there is a branch of your code with an unhandled return or bad flow if you use return nodes.

In situations like where a programmer may add a pin to a Sequence node or add logic after a for loop completes but the loop iteration might return early, this can often result in an accidental error in code flow. The warnings the Blueprint compiler will alert everyone of these issues immediately.

<a name="3.3.3"></a>
<a name="bp-graphs-funcs-node-limit"></a>
#### 3.3.3 No Function Should Have More Than 50 Nodes

Simply, no function should have more than 50 nodes. Any function this big should be broken down into smaller functions for readability and ease of maintenance.

The following nodes are not counted as they are deemed to not increase function complexity:

* Comment
* Route
* Cast
* Getting a Variable
* Breaking a Struct
* Function Entry
* Self

<a name="3.3.4"></a>
<a name="bp-graphs-funcs-description"></a>
#### 3.3.4 All Public Functions Should Have A Description

This rule applies more to public facing or marketplace blueprints, so that others can more easily navigate and consume your blueprint API.

Simply, any function that has an access specificer of Public should have its description filled out.

<a name="3.3.5"></a>
<a name="bp-graphs-funcs-plugin-category"></a>
#### 3.3.5 All Custom Static Plugin `BlueprintCallable` Functions Must Be Categorized By Plugin Name

If your project includes a plugin that defines `static` `BlueprintCallable` functions, they should have their category set to the plugin's name or a subset category of the plugin's name.

For example, `Zed Camera Interface` or `Zed Camera Interface | Image Capturing`.

<a name="3.4"></a>
<a name="bp-graphs"></a>
### 3.4 Blueprint Graphs

This section covers things that apply to all Blueprint graphs.

<a name="3.4.1"></a>
<a name="bp-graphs-spaghetti"></a>
#### 3.4.1 No Spaghetti

Wires should have clear beginnings and ends. You should never have to mentally untangle wires to make sense of a graph. Many of the following sections are dedicated to reducing spaghetti.

<a name="3.4.2"></a>
<a name="bp-graphs-align-wires"></a>
#### 3.4.2 Align Wires Not Nodes

Always align wires, not nodes. You can't always control the size and pin location on a node, but you can always control the location of a node and thus control the wires. Straight wires provide clear linear flow. Wiggly wires wear wits wickedly. You can straighten wires by using the Straighten Connections command with BP nodes selected. Hotkey: Q

Good example: The tops of the nodes are staggered to keep a perfectly straight white exec line.
![Aligned By Wires](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-good.png?raw=true "Aligned By Wires")

Bad Example: The tops of the nodes are aligned creating a wiggly white exec line.
![Bad](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-bad.png?raw=true "Wiggly")

Acceptable Example: Certain nodes might not cooperate no matter how you use the alignment tools. In this situation, try to minimize the wiggle by bringing the node in closer.
![Acceptable](https://github.com/Allar/ue5-style-guide/blob/main/images/bp-graphs-align-wires-acceptable.png?raw=true "Acceptable")

<a name="3.4.3"></a>
<a name="bp-graphs-exec-first-class"></a>
#### 3.4.3 White Exec Lines Are Top Priority

If you ever have to decide between straightening a linear white exec line or straightening data lines of some kind, always straighten the white exec line.

<a name="3.4.4"></a>
<a name="bp-graphs-block-comments"></a>
#### 3.4.4 Graphs Should Be Reasonably Commented

Blocks of nodes should be wrapped in comments that describe their higher-level behavior. While every function should be well named so that each individual node is easily readable and understandable, groups of nodes contributing to a purpose should have their purpose described in a comment block. If a function does not have many blocks of nodes and its clear that the nodes are serving a direct purpose in the function's goal, then they do not need to be commented as the function name and  description should suffice.

<a name="3.4.5"></a>
<a name="bp-graphs-cast-error-handling"></a>
#### 3.4.5 Graphs Should Handle Casting Errors Where Appropriate

If a function or event assumes that a cast always succeeds, it should appropriately report a failure in logic if the cast fails. This lets others know why something that is 'supposed to work' doesn't. A function should also attempt a graceful recover after a failed cast if it's known that the reference being casted could ever fail to be casted.

This does not mean every cast node should have its failure handled. In many cases, especially events regarding things like collisions, it is expected that execution flow terminates on a failed cast quietly.

<a name="3.4.6"></a>
<a name="bp-graphs-dangling-nodes"></a>
#### 3.4.6 Graphs Should Not Have Any Dangling / Loose / Dead Nodes

All nodes in all blueprint graphs must have a purpose. You should not leave dangling blueprint nodes around that have no purpose or are not executed.

**[⬆ Back to Top](#table-of-contents)**


<a name="4"></a>
<a name="Static Meshes"></a>
<a name="s"></a>
## 4. Static Meshes

This section will focus on Static Mesh assets and their internals.

<a name="4.1"></a>
<a name="s-uvs"></a>
### 4.1 Static Mesh UVs

If Linter is reporting bad UVs and you can't seem to track it down, open the resulting `.log` file in your project's `Saved/Logs` folder for exact details as to why it's failing. I am hoping to include these messages in the Lint report in the future.

<a name="4.1.1"></a>
<a name="s-uvs-no-missing"></a>
#### 4.1.1 All Meshes Must Have UVs

Pretty simple. All meshes, regardless how they are to be used, should not be missing UVs.

<a name="4.1.2"></a>
<a name="s-uvs-no-overlapping"></a>
#### 4.1.2 All Meshes Must Not Have Overlapping UVs for Lightmaps

Pretty simple. All meshes, regardless how they are to be used, should have valid non-overlapping UVs.

<a name="4.2"></a>
<a name="s-lods"></a>
### 4.2 LODs Should Be Set Up Correctly

This is a subjective check on a per-project basis, but as a general rule any mesh that can be seen at varying distances should have proper LODs.

<a name="4.3"></a>
<a name="s-modular-snapping"></a>
### 4.3 Modular Socketless Assets Should Snap To The Grid Cleanly

This is a subjective check on a per-asset basis, however any modular socketless assets should snap together cleanly based on the project's grid settings.

It is up to the project whether to snap based on a power of 2 grid or on a base 10 grid. However if you are authoring modular socketless assets for the marketplace, Epic's requirement is that they snap cleanly when the grid is set to 10 units or bigger.

<a name="4.4"></a>
<a name="s-collision"></a>
### 4.4 All Meshes Must Have Collision

Regardless of whether an asset is going to be used for collision in a level, all meshes should have proper collision defined. This helps the engine with things such as bounds calculations, occlusion, and lighting. Collision should also be well-formed to the asset.

<a name="4.5"></a>
<a name="s-scaled"></a>
### 4.5 All Meshes Should Be Scaled Correctly

This is a subjective check on a per-project basis, however all assets should be scaled correctly to their project. Level designers or blueprint authors should not have to tweak the scale of meshes to get them to confirm in the editor. Scaling meshes in the engine should be treated as a scale override, not a scale correction.

**[⬆ Back to Top](#table-of-contents)**


<a name="5"></a>
<a name="Niagara"></a>
<a name="ng"></a>
## 5. Niagara

This section will focus on Niagara assets and their internals.

<a name="5.1"></a>
<a name="ng-rules"></a>
### 5.1 No Spaces, Ever

As mentioned in [00.1 Forbidden Identifiers](#00), spaces and all white space characters are forbidden in identifiers. This is especially true for Niagara systems as it makes working with things significantly harder if not impossible when working with HLSL or other means of scripting within Niagara and trying to reference an identifier.

(Original Contribution by [@dunenkoff](https://github.com/Allar/ue5-style-guide/issues/58))


**[⬆ Back to Top](#table-of-contents)**


<a name="6"></a>
<a name="Levels"></a>
<a name="levels"></a>
## 6. Levels / Maps

[See Terminology Note](#terms-level-map) regarding "levels" vs "maps".

This section will focus on Level assets and their internals.

<a name="6.1"></a>
<a name="levels-no-errors-or-warnings"></a>
### 6.1 No Errors Or Warnings

All levels should load with zero errors or warnings. If a level loads with any errors or warnings, they should be fixed immediately to prevent cascading issues.

You can run a map check on an open level in the editor by using the console command "map check".

Please note: Linter is even more strict on this than the editor is currently, and will catch load errors that the editor will resolve on its own.

<a name="6.2"></a>
<a name="levels-lighting-should-be-built"></a>
### 6.2 Lighting Should Be Built

It is normal during development for levels to occasionally not have lighting built. When doing a test/internal/shipping build or any build that is to be distributed however, lighting should always be built.

<a name="6.3"></a>
<a name="levels-no-visible-z-fighting"></a>
### 6.3 No Player Visible Z Fighting

Levels should not have any [z-fighting](https://en.wikipedia.org/wiki/Z-fighting) in all areas visible to the player.

<a name="6.4"></a>
<a name="levels-mp-rules"></a>
### 6.4 Marketplace Specific Rules

If a project is to be sold on the UE4 Marketplace, it must follow these rules.

<a name="6.4.1"></a>
<a name="levels-mp-rules-overview"></a>
#### 6.4.1 Overview Level

If your project contains assets that should be visualized or demoed, you must have a map within your project that contains the name "Overview".

This overview map, if it is visualizing assets, should be set up according to [Epic's guidelines](http://help.epicgames.com/customer/en/portal/articles/2592186-marketplace-submission-guidelines-preparing-your-assets#Required%20Levels%20and%20Maps).

For example, `InteractionComponent_Overview`.

<a name="6.4.2"></a>
<a name="levels-mp-rules-demo"></a>
#### 6.4.2 Demo Level

If your project contains assets that should be demoed or come with some sort of tutorial, you must have a map within your project that contains the name "Demo". This level should also contain documentation within it in some form that illustrates how to use your project. See Epic's Content Examples project for good examples on how to do this.

If your project is a gameplay mechanic or other form of system as opposed to an art pack, this can be the same as your "Overview" map.

For example, `InteractionComponent_Overview_Demo`, `ExplosionKit_Demo`.

**[⬆ Back to Top](#table-of-contents)**


<a name="7"></a>
<a name="textures"></a>
## 7. Textures

This section will focus on Texture assets and their internals.

<a name="7.1"></a>
<a name="textures-dimensions"></a>
### 7.1 Dimensions Are Powers of 2

All textures, except for UI textures, must have its dimensions in multiples of powers of 2. Textures do not have to be square.

For example, `128x512`, `1024x1024`, `2048x1024`, `1024x2048`, `1x512`.

<a name="7.2"></a>
<a name="textures-density"></a>
### 7.2 Texture Density Should Be Uniform

All textures should be of a size appropriate for their standard use case. Appropriate texture density varies from project to project, but all textures within that project should have a consistent density.

For example, if a project's texture density is 8 pixel per 1 unit, a texture that is meant to be applied to a 100x100 unit cube should be 1024x1024, as that is the closest power of 2 that matches the project's texture density.

<a name="7.3"></a>
<a name="textures-max-size"></a>
### 7.3 Textures Should Be No Bigger than 8192

No texture should have a dimension that exceeds 8192 in size, unless you have a very explicit reason to do so. Often, using a texture this big is simply just a waste of resources.

<a name="7.4"></a>
<a name="textures-group"></a>
### 7.4 Textures Should Be Grouped Correctly

Every texture has a Texture Group property used for LODing, and this should be set correctly based on its use. For example, all UI textures should belong in the UI texture group.

**[⬆ Back to Top](#table-of-contents)**


## Major Contributors

* [Michael Allar](http://allarsblog.com): [GitHub](https://github.com/Allar), [Twitter](https://twitter.com/michaelallar)
* [CosmoMyzrailGorynych](https://github.com/CosmoMyzrailGorynych)
* [billymcguffin](https://github.com/billymcguffin)
* [akenatsu](https://github.com/akenatsu)

## License

Copyright (c) 2016 Gamemakin LLC

See [LICENSE](/LICENSE)

**[⬆ Back to Top](#table-of-contents)**


## Amendments

We encourage you to fork this guide and change the rules to fit your team's style guide. Below, you may list some amendments to the style guide. This allows you to periodically update your style guide without having to deal with merge conflicts.

# };
