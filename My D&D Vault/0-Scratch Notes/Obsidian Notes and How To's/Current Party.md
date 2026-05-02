---
transportation: rhinoceros
speed: fast
exhaustionLevel: 0
hoursPerDay: 8
---
#### Example 

This party is traveling by `= this.transportation`. (calls from this page)

This party is traveling by `= [[Transporation]].movement[this.transportation].name`. (calls from different page)

It has a base speed of `= [[Transporation]].movement[this.transportation].base` and takes `= [[Transporation]].movement[this.transportation].normal` minutes to go one mile.

#### Calculate Speed 

Miles per hour using current method of travel: `= round(160 * ([[Transporation]].movement[[[Current Party]].transportation][[[Current Party]].speed] * choice([[Current Party]].exhaustionLevel > 1, 2, 1)) / 60 / [[Current Party]].hoursPerDay, 0)`

Current method of travel's speed: `= [[Transporation]].movement[[[Current Party]].transportation][[[Current Party]].speed]`

Party's Exhaustion Level: `= [[Current Party]].exhaustionLevel`

Hours per Day: `= [[Current Party]].hoursPerDay`

(Distance x method of travel's speed x party's exhaustion level / 60 minutes per hour / hours per day )


