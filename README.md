# Better_Gunplay

**TL;DR:**
1.  **Locate Parameter:** Find the `TargetDeadType` value used for enemy kills in `SkillTable.uasset`.
2.  **Trace Reference:** Based on this value, locate the corresponding `...DeadShow` parameter in `CharacterDeadTable.uasset`.
3.  **Check Files:** Examine the files in the `SB/Content/Art/Show/Dead` path pointed to by the parameter. **Confirm if a version containing `NoTimeScale` exists.**
4.  **Modify Configuration:**
    *   **If exists:** Directly replace the `...DeadShow` parameter value with the path to this `NoTimeScale` version.
    *   **If doesn't exist:** Manually modify the content of the original file to remove the time scaling effect.

---

**How to disable the slow-motion effect for remote enemy kills in *Stellar Blade*?**
> **Note:** This is a summary of the final solution. **No relevant tutorials were found** when attempting to solve this issue, and practical exploration revealed that the disabling process is **significantly more complex** than the steps outlined here.

1.  **Locate Key Parameter:**  
    First, examine the `SkillTable.uasset` file. All entries containing `'P_Eve_Gun_Shoot'` have their `'TargetDeadType'` parameter set to `'Custom6'`. It is therefore inferred that the death type for all enemies killed by firearms is `'Custom6'`.

2.  **Trace `Custom6` Reference:**  
    Search game files for where `'Custom6'` is used, locating the `'CharacterDeadTable.uasset'` file. Within this file, the `'Custom6DeadShow'` parameter is found, with possible values `"Dead/Dead_Monster_SkillType_Range1"` or `"Dead/Dead_Monster_SkillType_Range1NoTimeScale"`.

3.  **Analyze Related Resource Files:**  
    Use the Fmodel tool to inspect files in the game resource path `SB/Content/Art/Show/Dead`. Confirm the existence of `"Dead_Monster_SkillType_Range1.uasset"` and `"Dead_Monster_SkillType_Range1NoTimeScale.uasset"`. Comparing these files reveals their primary difference lies in the `TimeScale` value and the presence of `'NoTimeScale'` in the filename. It is thus inferred that these files control whether a slow-motion (time scaling) effect is triggered upon enemy death.

4.  **Modify Configuration:**  
    Return to the `'CharacterDeadTable.uasset'` file and **change all** `'Custom6DeadShow'` parameter values to `"Dead/Dead_Monster_SkillType_Range1NoTimeScale.uasset"`.

5.  **Verify Effect:**  
    Launch the game and test. Confirm that the slow-motion effect for remote enemy kills has been successfully disabled.
