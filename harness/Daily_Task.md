# Daily Task

Date: 2026-06-10

## Today UE Task

InventoryItems（背包物品数组），类型为 String Array（字符串数组）。

## Goal

拾取 BP_InteractBox 后，把物品名加入 InventoryItems，并让 ItemHUD 显示 InventoryItems 的长度。

## Steps

1. 在 BP_ThirdPersonCharacter 中创建变量 InventoryItems，类型为 String Array。
2. 在拾取成功逻辑处，将字符串 InteractBox Add 到 InventoryItems。
3. 更新 ItemHUD 时读取 Length(InventoryItems)，显示为 Item: 数组长度。
4. 拾取成功后 Print String：InventoryItems[0] = InteractBox。

## Done When

- 初始 HUD 显示 Item: 0。
- 对 BP_InteractBox 按 E 后，HUD 显示 Item: 1。
- 屏幕打印 InventoryItems[0] = InteractBox。

## Rule

完成后再记录；未完成不记录、不催。

## Status

已完成：2026-06-10。
