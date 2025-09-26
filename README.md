# Better_Gunplay
# How to Disable Slow Motion on Ranged Kills in *Stellar Blade*

## TL;DR (Too Long; Didn't Read)
1. **Locate Parameter**: Find the `TargetDeadType` value used for killing enemies in `SkillTable.uasset`.  
2. **Trace Reference**: Using this value, locate the corresponding `...DeadShow` parameter in `CharacterDeadTable.uasset`.  
3. **Check Assets**: Verify if a `NoTimeScale` version of the file exists at the path referenced by the parameter (`SB/Content/Art/Show/Dead`).  
4. **Modify Configuration**:  
   - *If exists*: Replace the `...DeadShow` parameter value with the path to the `NoTimeScale` version.  
   - *If absent*: Manually edit the original asset to remove the time scaling effect.  

> **Note**: *This is a condensed solution summary. Actual implementation proved significantly more complex than described, with no existing tutorials available during troubleshooting.*

---

## Detailed Implementation Steps

### 1. Locate Critical Parameter
- Inspect `SkillTable.uasset`.  
- All entries containing `'P_Eve_Gun_Shoot'` have their `'TargetDeadType'` parameter set to **`'Custom6'`**.  
- **Conclusion**: All ranged weapon kills use the death type `Custom6`.

### 2. Trace `Custom6` Reference
- Search game files for references to `'Custom6'`.  
- Locate `CharacterDeadTable.uasset`.  
- Identify the `'Custom6DeadShow'` parameter. Its possible values are:  
  - `"Dead/Dead_Monster_SkillType_Range1"`  
  - `"Dead/Dead_Monster_SkillType_Range1NoTimeScale"`.

### 3. Analyze Asset Files
- Use **Fmodel** to inspect assets under `SB/Content/Art/Show/Dead`.  
- Confirm existence of both:  
  - `Dead_Monster_SkillType_Range1.uasset`  
  - `Dead_Monster_SkillType_Range1NoTimeScale.uasset`  
- **Key Difference**: The `NoTimeScale` variant lacks time-scaling effects (evident in its `TimeScale` value and filename).

### 4. Modify Configuration
- Edit `CharacterDeadTable.uasset`.  
- Replace **ALL** instances of the `'Custom6DeadShow'` parameter value with:  
  `"Dead/Dead_Monster_SkillType_Range1NoTimeScale.uasset"`.

### 5. Verify Results
- Launch the game and test ranged kills.  
- **Expected Outcome**: Slow-motion effects during enemy deaths are disabled.
