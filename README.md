# Capture the Data Flag

## The Data

The current dataset consists of data from international figure skating competitions. These have been split into the following individual files and can be downloaded at the relevant links:

- [skaters](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Skaters.csv)
- [events](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Events.csv)
- [elements](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Elements.csv)
- [components](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Components.csv)
- [jumps](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Jumps.csv)
- [spins_steps](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Spins_Steps.csv)

---

## skaters

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Skaters.csv)

The skaters data is a list of every individual skater that is found in the data as well as fields that are relevant to them as a skater.

#### Data Dictionary:

- name: the name of the skater in the format: SURNAME FirstName
- nationality: the 3-digit country code that the skater represents
- gender: either M or W depending on which division the skater competes in

## events

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Events.csv)

THe events data shows which events are included in the data as well as fields that describe when and where the event fell.

#### Data Dictionary:

- competition: the name of the competition
- year: the year that the competition took place in the format: YYYY
- month: the name of the month the competition took place
- season: which skating season the event falls into in the foramt: Season YYYY/YY
- location: the name of the country where the event took place

## elements

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Elements.csv)

The elements data is the results of each element that the skater performs in their routine. Each element has a code that links back to the Jumps and spins_steps data for the description of the element. For example, the element code `3A` refers to a triple (3) axel (A) jump, and the element code `FCSp4` refers to a flying (F) camel (C) spin (Sp) level 4 (4). A jump will always start with the number of revolutions, whilst a Spin or Step element will end with the number that corresponds to the element level. If a jump is done in a combination or sequence, then a + will be between each individual jump that makes up the combined element, such as `2A+2L` being a double axel - double loop combo.

Each element has a `baseValue` which is determined which element was attempted and landed. This can vary from the `baseValue` in the Jumps of spins_steps data based on the `notes` field or an adjustment in the code of the element itself. The following are these adjustments:

| code  | description                       | adjustment       |
| ----- | --------------------------------- | ---------------- |
| COMBO | Jump Combination Downgrade        | baeValue - 20%   |
| SEQ   | Jump Sequence Downgrade           | baseValue - 20%  |
| REP   | Repeated Jump                     | baseValue - 30%  |
| \*    | Invalid Element                   | baseValue = 0.00 |
| <     | Under-rotated jump                | baseValue - 20%  |
| <<    | Downgraded jump                   | Minus 1 Level    |
| x     | Credit for highlight distribution | baseValue + 10%  |
| e     | Incorrect edge                    | baseValue - 20%  |
| !     | Unclear edge                      | goe impact       |
| q     | Jump lnded on quarter             | goe impact       |
| V     | Unclear flying entry              | goe impact       |

The first three, `COMBO`, `SEQ`, and `REP` are all found in the element code, and the remaining are found in the notes column of the data. These can be used to determine if the `baseValue` in the elements data is correct by making the adjustment from the `baseValue` in the respective Jumps or Spins_Steps data. The notes either adjust the `baseValue` that would normally be awarded for the element, or have `goe` impact from the judges. The only other result is the downgraded jump (`<<`) note, which takes a jump element and subtracts 1 from its number. An example is a triple salchow (`3S`) with `<<` will be awarded the `baseValue` of a double salchow (`2S`).

This `baseValue` is then multiplied by the `goe` or grade of execution which is how well the judges deemed the element to be executed. The resulting number is the total score for the given element.

#### Data Dictionary:

- id: the unique id for the element row
- name: the name of the figure skater performing the element in the format: SURNAME FirstName
- year: the year that the element was performed in the format: YYYY
- competition: the name of the competition that the element was performed in
- skate: if the element was in the Short Program (SP) or the Free Program (FP)
- element: the code for the element
- baseValue: the numerical base value awarded for the element (this plus the goe is to total score for the element)
- goe: the numerical grade of exectution awarded to the element (this plus the baseValue is the total score for the element)
- notes: any info flags that impact(ed) the base value or goe

## components

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Components.csv)

The components data looks at five aspects of a skaters performance and marks them on a scale of 1-10 with 10 being the best. This `baseValue` is then multiplied by the `factor` for the component score as different events and difference competitions have difference factors. The component will be one of `SkatingSkills`, `Transitions`, `Performance`, `Composition`, or `Interpretation`.

In addition, there are three difference deductions that can be applied to a routine. These have the component name of `DeductionsFalls`, `DeductionsTime`, or `DeductionsLateStart`. The deductions works exactly the same as any other component, except that their `baseValue` is negative. For example, if a skater falls twice, then the `DeductionsFalls` value will be -1.00. All deductions have a multiplicatory `factor` of 1.00.

#### Data Dictionary:

- id: the unique id for the component row
- name: the name of the figure skater achieving the component in the format: SURNAME FirstName
- year: the year that the component was achieved in the format: YYYY
- competition: the name of the competition that the component was awarded in
- skate: if the component was in the Short Program (SP) or the Free Program (FP)
- component: the name of the component
- baseValue: the numerical base value awarded for the component (this is multiplied by the factor for the total component score)
- factor: the numerical scaling applied to the component (this is multiplied by the baseValue for the total component score)

## jumps

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Jumps.csv)

The jumps data contains the code for every jump that is listed in the data, as well as the corresponding `baseValue` that would be awarded for the jump.

#### Data Dictionary:

- code: the code for the jump element
- element: the name for the jump element
- baseValue: the base value awarded for the jump

## spins_steps

[DOWNLOAD LINK](https://capture-the-data-flag.s3.ap-southeast-2.amazonaws.com/Spins_Steps.csv)

The spins_steps data contains the code for each spin/step that is listed in the data. These codes are for the spin or step that is attempted and the level can be found across the columns. For example, a Flying Combo Spin has the code `FCoSp`, and if it is performed at a Level 3 (`FCoSp3`), then its `baseValue` can be found in the `L3` column (2.50). If the spin has the `V` adjustment, then this same spin's `baseValue` could be found in the `L3V` column (1.88).

#### Data Dictionary:

- code: the code for the spin or step element
- element: the name for the spin or step element
- type: whether it is a Spin or Sequence row
- B: the numerical value awarded for a Base element
- BV: the numerical value awarded for a Base element with a V info
- L1: the numerical value awarded for a Level 1 element
- L1V: the numerical value awarded for a Level 1 element with a V info
- L2: the numerical value awarded for a Level 2 element
- L2V: the numerical value awarded for a Level 2 element with a V info
- L3: the numerical value awarded for a Level 3 element
- L3V: the numerical value awarded for a Level 3 element with a V info
- L4: the numerical value awarded for a Level 4 element
- L4V: the numerical value awarded for a Level 4 element with a V info

---

## The Challenges

There are five challenges currently created for this capture-the-data-flag event. The [Getting_Started](getting_started.ipynb) python notebook has some initial code to install the relevant Python libraries and show how to access the data from the S3 bucket. This is not a restriction and is simply a support tool for those less familiar with data processing or Python.

Each challenge is worth a different number of points (equal to the challenge number), increasing throughout the challenges to reflect the increasing difficulty of the challenge.

## Challenge 1 - 1 Point

## Challenge 2 - 2 Points

## Challenge 3 - 3 Points

## Challenge 4 - 4 Points

## Challenge 5 - 6 Points
