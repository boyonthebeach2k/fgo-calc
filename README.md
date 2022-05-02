# fgo-calc

Damage, Refund and Stargen calculator for player and enemy characters from Fate/Grand Order

## Example

#### Calc an example string

```typescript
import { ApiConnector, Language, Region, Servant, Enemy } from "@atlasacademy/api-connector";
import { calcSvt } from "fgo-calc";

const cacheDuration = 20 * 1000;
const apiConnector = new ApiConnector({
    host: "https://api.atlasacademy.io",
    region: Region.JP,
    language: Language.ENGLISH,
});

const commandString = `L100 | c2000 cd20 /*L100 grudge match*/ | a44 am20 /*skills 1&2*/ |
    a40 ng45 sg50 /*bride1*/ | a50 /*casumu s3*/ | a40 ng45 sg50 /*bride1 dies, enter bride2*/ |
    npqb d-20 | a36 n18 /*arctic L9*/ | caster sky hp187863 | card1 d20 #turn3`;

function getSvt(id: number): Promise<Servant.Servant | Enemy.Enemy> {
    return apiConnector.servant(id, false, cacheDuration);
}

getSvt(100500).then(calcSvt(svt, commandString));
```

#### Get human-readable help messages

```typescript
import { cmdArgs } from "fgo-calc";

cmdArgs();
```

---

Data sourced from [Atlas Academy](https://atlasacademy.io).
