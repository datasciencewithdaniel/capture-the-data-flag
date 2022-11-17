# Capture the Data Flag

## The Data

The current dataset consists of data from international figure skating competitions. These have been split into the following individual files and can be downloaded at the relevant links:

- [skaters](###-skaters)
- [events](###-events)
- [elements](###-elements)
- [components](###-components)
- [jumps+info](###-jumps+info)
- [spins+steps](###-spins+steps)

---

### skaters

[DOWNLOAD LINK]()

- name: the name of the skater in the format: SURNAME FirstName
- nationality: the 3-digit country code that the skater represents
- gender: either M or W depending on which division the skater competes in

### events

[DOWNLOAD LINK]()

- competition: the name of the competition
- year: the year that the competition took place in the format: YYYY
- month: the name of the month the competition took place
- season: which skating season the event falls into in the foramt: Season YYYY/YY
- location: the name of the country where the event took place

### elements

[DOWNLOAD LINK]()

- id: the unique id for the element row
- name: the name of the figure skater performing the element in the format: SURNAME FirstName
- year: the year that the element was performed in the format: YYYY
- competition: the name of the competition that the element was performed in
- skate: if the element was in the Short Program (SP) or the Free Program (FP)
- element: the code for the element
- baseValue: the numerical base value awarded for the element (this plus the goe is to total score for the element)
- goe: the numerical grade of exectution awarded to the element (this plus the baseValue is the total score for the element)
- notes: any info flags that impact(ed) the base value or goe

### components

[DOWNLOAD LINK]()

- id: the unique id for the component row
- name: the name of the figure skater achieving the component in the format: SURNAME FirstName
- year: the year that the component was achieved in the format: YYYY
- competition: the name of the competition that the component was awarded in
- skate: if the component was in the Short Program (SP) or the Free Program (FP)
- component: the name of the component
- baseValue: the numerical base value awarded for the component (this is multiplied by the factor for the total component score)
- factor: the numerical scaling applied to the component (this is multiplied by the baseValue for the total component score)

### jumps+info

[DOWNLOAD LINK]()

- code: the code for the jump element or info note
- element: the name for the jump element or info note
- type: whether it is a Jump or Info row
- baseValue: the base value awarded for the jump or the adjustment made for the info note

### spins+steps

[DOWNLOAD LINK]()

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
