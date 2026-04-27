# SalishMesh Repeater Taxonomy

A shared vocabulary and grading framework for describing MeshCore repeater installations on SalishMesh.

**Status:** working draft, circulating for community feedback.

## Purpose

Repeaters in SalishMesh vary widely. A stock device on a balcony and a custom-built rooftop install with signal filters and a Pi steward are both "repeaters" in casual usage, but they have very different capabilities and operational characteristics. The word has stopped doing useful work.

This taxonomy aims to do three things:

1. **Establish shared terminology.** When someone says "elevated install with a B-grade antenna and 7/10 sightlines," everyone reading should picture roughly the same thing.
2. **Enable apples-to-apples comparison.** Each repeater gets a profile graded across the same axes.
3. **Surface upgrade paths.** Grades are non-judgmental but directional. A C-grade antenna isn't bad, it's just a clear path to B-grade for very little money.

A stock repeater on a balcony is welcome and useful. So is a custom rooftop install. They aren't the same thing, and the framework should make that visible without shaming the smaller setup.

## The framework

A repeater profile is graded across **eight axes**. Some are categorical (pick one). Others are graded A through D, where A is the highest-capability install. Grades reflect the installation, not the operator.

1. Power source
2. TX power
3. Hardware
4. Antenna
5. Elevation
6. Shelter
7. Sightlines
8. Updates

## Axes

### 1. Power source

Categorical. How the node is powered.

- **Solar.** Solar panel and battery, no grid connection.
- **AC.** Plugged into mains, no battery.
- **AC + battery.** Mains with battery backup for outages.
- **Solar + AC.** Solar primary, mains backup for low-sun periods.
- **Battery only.** Internal battery, no recharge source. Rare.

### 2. TX power

Categorical. Conducted output from the radio board, measured at the SMA connector before the antenna. Antenna gain is graded separately.

- **Low-power.** Sub-1W. Typical of solar-class boards (Solar Pro, RAK Solar Mini).
- **Full-power.** 1W. Standard ISM ceiling for unlicensed operation.
- **High-power.** 4W. Station G2 class.

Note: EIRP (what actually radiates) is TX power plus antenna gain. Canadian RSS-247 caps unlicensed EIRP at 36 dBm. A full-power node with a high-gain antenna can hit that ceiling.

### 3. Hardware

The board model and whether it is stock or modified. Common boards on SalishMesh:

- Seeed Solar Pro
- RAK Solar Mini
- Heltec V4
- Ikoka Stick
- Station G2

Note major component upgrades inline (upgraded solar panel, larger battery, custom enclosure). Antenna gets its own axis.

### 4. Antenna

Graded A through D by gain. Listed in dBi.

| Grade | dBi | Example |
|---|---|---|
| A | 8+ | 12 dBi Diamond, well-tuned upgrades |
| B | 5 to 7 | 5 dBi Alfa, common upgrade size |
| C | 3 to 4 | Modest upgrade |
| D | stock (~2) | Out-of-box stock antenna |

DIY antennas are noted separately and graded on measured performance.

### 5. Elevation

Graded A through D by physical height of the node. Independent of shelter and sightlines.

| Grade | Description |
|---|---|
| A | Peak, summit, ridge, or rooftop on a tall building |
| B | Standard rooftop, hilltop residential |
| C | Upper floor (5th and above) |
| D | Lower floor (1st through 4th), ground level, basement |

### 6. Shelter

Graded A through D by the RF environment immediately around the node. Independent of elevation.

| Grade | Description |
|---|---|
| A | Outdoor, no obstruction |
| B | Outdoor with partial obstruction (tree canopy, eaves) |
| C | Indoor through windows on multiple sides |
| D | Indoor through a single window or no window |

### 7. Sightlines

A score from 1 to 10 with a brief geometry note. The score reflects effective usable horizon, accounting for direction, blockage, and surrounding terrain. The note captures the geometry.

Examples:

- 9/10 (360°, ridge, no nearby blockage)
- 7/10 (360°, rooftop, surrounded by 12-story buildings)
- 5/10 (180° NW, balcony)
- 3/10 (90° W, through tree canopy)

### 8. Updates

Graded by the highest-capability update path available. Walk-up USB is always implicit and only listed when it is the only path.

| Grade | Method |
|---|---|
| A | Mesh OTA (future, not yet deployed) |
| B | Pi steward |
| C | Bluetooth (flashable from phone within RF range) |
| D | USB only (walk-up access required) |

A **Pi steward** is a Raspberry Pi (typically) running RepeaterWatch alongside the repeater, providing remote update capability and other supporting services. RepeaterWatch link TBD.

## Profile format

Each repeater has its own directory in this repo containing a `profile.md`. Format:

```
# Node Name

  Power Source: solar
  TX Power:     low-power
  Hardware:     Seeed Solar Pro (stock)
  Antenna:      8 dBi, Grade A
  Elevation:    rooftop, Grade B
  Shelter:      outdoor, Grade A
  Sightlines:   7/10 (360°, surrounded by 12-story buildings)
  Updates:      USB only, Grade D

## Notes

Optional free-form notes about the install, location, history, anything
relevant to the site.
```

## Example profile

# Olympic Village

  Power Source: solar
  TX Power:     low-power
  Hardware:     Seeed Solar Pro (stock)
  Antenna:      8 dBi, Grade A
  Elevation:    rooftop on 5-story building, Grade B
  Shelter:      outdoor, Grade A
  Sightlines:   7/10 (360°, surrounded by 12-story buildings)
  Updates:      USB only, Grade D

## Notes

Solar Pro on the Olympic Village rooftop. Surrounded by tall residential buildings on several sides, which limits range despite the upgraded antenna and outdoor placement. Clear upgrade path is to add a Pi steward to bring Updates from D to B.

---

## Open questions

1. Should Hardware itself be graded (e.g., Solar Pro vs RAK Solar Mini), or is listing the model enough? Component-level grades (panel, battery, enclosure) might be a future addition.
2. Are eight axes the right number, or should any be merged?
3. Does the A through D scale need a fifth tier for exceptional installs?
4. RepeaterWatch scope and naming. The Pi steward role currently points at RepeaterWatch (Jessy and Chris). Confirming this with them before publishing.
