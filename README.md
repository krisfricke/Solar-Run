# SOLAR RUN — a torch-ship trading game around one star

**Play it: <https://krisfricke.github.io/Solar-Run/>**

**vS1.13.1** — a single-file HTML game (needs a network connection on first load for the
Three.js CDN). The companion piece to [Interstellar Trail](https://krisfricke.github.io/Interstellar-Trail/),
one level down the well.

Same trading soul, entirely different physics: twelve ports around Sol — Mercury, Venus,
Earth, Luna, Mars, Ceres, Ganymede, Titan, Uranus, Neptune, Pluto — every one on its real
orbit, moving as the clock runs. Start at Earth with 200 cr and a used Space Hilux. The
Grand Tour: dock at all 11 and return to Earth; ranked by % ROI per day.

## The physics
- **Live Keplerian ephemerides**: JPL/Standish approximate elements for the planets (plus
  Ceres and Pluto), propagated from J2000 to **the real date and time you press LAUNCH** — the planets are where they actually are in your sky (comfortably inside the elements' 1800–2050 validity window), then advance with game time; Luna even rides her true mean longitude; Luna, Ganymede and
  Titan ride circular orbits about their primaries. Earth–Mars really swings 0.66–2.5 AU:
  launch windows are real, and prices (which radiate from each good's source by *current*
  distance) breathe with the geometry.
- **Brachistochrone intercepts of moving targets.** Constant thrust, flip at the midpoint:
  t = 2√(d/a), thrust fixed so a ∝ 1/mass. The solver iterates the arrival time in the
  frame co-moving with your departure body (you leave carrying its orbital velocity), so
  the chord is the origin-relative separation at the moment of arrival.
- **Calibration: Earth orbit → Luna, empty Taurean-Mule spec (mass 100), exactly 1 hour** —
  including the gravity-well terms. That pins the torch at a₀ ≈ 120.8 m/s² (~12 g).
  Mars at opposition ~13 h; Pluto ~5 days; peak speeds in the hundreds to thousands of km/s.
- **Gravity effects live where they matter at 12 g: the wells.** Departure pays (√2−1)·v_orb
  climbing from parking orbit to escape; arrival pays the same shaping the capture. En route,
  the Sun pulls 0.006 m/s² against a 120 m/s² burn — negligible, and honestly ignored.
- **Relativity is modeled** — because at these speeds it finally, marginally, matters.
  Peaks: Moon hop 215 km/s (2.6 ls/h — 0.3 ms of dilation, Newton forgiven), Pluto ~0.083c
  (~8 min over the trip), the Voyager pilgrimage 0.185c (11.1 lm/h — the ship clock runs
  ~88 minutes slow over 10.6 days), a stripped Orion sprint 0.34c (~2.7 hours of youth).
  Proper time is integrated exactly over the piecewise burn plan (dτ = v²/2c² dt, first
  order; fully relativistic kinematics would stretch the extreme runs another ~2-3%, which
  we note and decline). The status bar keeps a running ship-clock-vs-standard counter, the
  HUD shows velocity in ls/h (escalating to lm/h past one light-minute per hour) and in
  fractions of c — and, the important part, CARGO AGES BY SHIP TIME. Mangos on the Orion
  sprint survive at ~16% instead of ~13%: relativity preserves fruit. Fractional survivors
  are settled by lottery (the last mango either rotted or it didn't), so the museum
  fresh-fruit run is a gamble that time dilation genuinely improves.
- **The delicate arrival**: if your current braking authority can shape v_orb inside a
  five-minute burn, you arrive *tangent to the destination's outer atmosphere at exactly
  circular orbital speed* — logged as "clean as a kiss," no fees. Too heavy (an ore-laden
  Mule at Neptune, say, where v_orb is 16.3 km/s) and you wallow into a graceless capture:
  +15 minutes and a tug fee. Cargo mass thus bites three times: trip time, escape odds,
  and the quality of your arrival.
- Mid-flight mass and thrust changes replan the remainder bang-bang optimally, overshoots
  and double-backs included — same honest machinery as the interstellar game.

## The solar exclusion zone
No ordinary hull may fly closer to the Sun than half Mercury's orbit (0.19 AU): routes that
would cross the zone detour around it on the true shortest path (tangent–arc–tangent, drawn
as a bow in the sky and charged honestly in time). The one exception is the **Icarus Class
Explorer** — solar-rated, certified to cut straight across the Sun's doorstep so long as it
doesn't actually touch (two solar radii), and its shielding halves CME losses. When inner
ports sit in opposition, the Icarus flies chords nobody else may.

## Voyager Station
The twelfth port: a museum grown around Voyager 1 on its real outbound track — 75.5 AU at
J2000 + 3.566 AU/yr toward Ophiuchus, ~170 AU today and receding at 17 km/s, so the
intercept solver must chase it. The Earth pilgrimage runs ~10.6 days empty, the longest
haul in the game, and the Grand Tour now includes it. The gift shop sells Golden Record
replica plates (engraved like the real one), whose whole value is that almost nobody has
one — demand halves per plate already sold in a market. Being a museum and not a colony,
the station buys ONLY what a remote museum can use — coffee, mangos, machine spares, water
ice, vaccine printers, and Earth media for morale — at prices befitting 170 AU of delivery
distance; everything else meets a polite "no buyers at a museum." Note the cruel arithmetic
of fresh fruit: mangos keep 4 days and the pilgrimage takes 10.6 at reference mass, so the
only way to land one alive is a stripped-down speedster sprint (an empty Orion arrives in
~5.7 days with ~13% of the crate intact). Delivering fresh mangos to Voyager Station is the
game's ultimate flex. Ceres, meanwhile, has begun exporting astergris — like ambergris, but from space;
where it comes from, no one is really sure, and Ceres isn't saying.

## The fleet, rechristened
The Silk Road's hulls sailed up the well: the **Astro-Cog** (100/100) is the reference
freighter now, the **Space-Faering** (50/83) the honest little starter boat, the **Astral
Carrack** (200/120), **Star Galleass** (300/132) and flagship **Space Galleon** (400/139)
the hauling ladder, and the **Interplanetary Galliot** holds the point-defense franchise. The **Icarus Solar Dhow** (75/75) carries the corona-line certification
and CME shielding, joined by its heavy sister the **Solar Barque** (150/130), which hauls
real cargo through the exclusion zone; Ra would approve. The **Space Coracle** (10/5) is
mechanically identical to an escape pod but purchasable — a vessel for philosophers — while
the Escape Pod itself is off the sales floor: fate issues those, chiefly via pirate
torpedoes, and losing even a Coracle leaves you in one. The difference was always the
choosing. The Flying Saucer, T'Khasi Orion and Apollo CSM keep their names, as relics
should.

## The Apollo CSM (museum-grade)
Earth's yard sells a lovingly restored Apollo Command/Service Module with its literal
historical propellant load: 2,800 m/s of delta-v, total, ever. In a game where the Moon
hop's brachistochrone spends ~68,000 m/s, this buys exactly one trajectory: the translunar
transfer it was born for, Earth ⇄ Luna in 3.05 days, ending in a guaranteed graceless
capture (it never could tangent-kiss; history records splashdowns). Every other destination
consults **THE SLINGSHOT ALMANAC**. Ownership also enrolls
your credits in the Quixotic Eccentrics Endowment — a guaranteed 6% per annum, compounded
over every year you drift, so a ten-year Ganymede chain nearly doubles your money while
you age gently at zero g. The CSM flies with its true silhouette (command-module cone,
service module, SPS bell), and Voyager Station renders as the probe itself — dish forever
pointed home, gold record glinting — inside the museum's observation lattice. It: a Tisserand-style flyby-sequence
search (circular-coplanar approximation, ≤3 assists among Venus/Earth/Mars/Jupiter/Saturn).
Ports sling departures to escape velocity and refuel the tanks, so the 2.8 km/s is pure
heliocentric currency; unpowered flybys retune v∞ by up to 2·v∞·sin(δmax/2) with resonant
pumping charged in time, aerocapture is free where there's air, and the giants brake you
into their own moons. Results rhyme with history: Venus direct (~2.5 km/s, 222 d), Mars
only via a Venus assist (2.4 yr — direct departure needs 2.88 km/s and the tank holds 2.80),
Ganymede on a ten-year Galileo-scale chain, and Mercury defeating three flybys entirely,
as it defeated everyone before MESSENGER. Voyager Station remains beyond chemical reach:
the museum stays exclusive. This is the one context where slingshots matter — the torch
ships never open the almanac. The intercept display also
now draws the TRUE chord's image under the compressed map — a straight display line used
to cut visually near the Sun on routes whose real perihelion was comfortably legal.

## Why no gravity slingshots?
Physics, not laziness. A flyby donates at most ~2x the assisting planet's orbital speed —
Jupiter, the best case in the system, is worth ~26 km/s. This ship peaks at 215 km/s on the
Moon hop and thousands of km/s on outer runs; an assist would save seconds while the detour
costs hours. Slingshots are the poor man's delta-v, and a 12-gee continuous torch is not
poor: at brachistochrone accelerations the straight line wins every route in the system. The Apollo CSM is the exception that
proves it: at 2,800 m/s, gravity assists aren't optimization, they're survival — but this
router only solves constant-thrust chords, so it cannot plot flyby chains (that's a
different optimizer entirely: porkchop plots and flyby sequencing, the art that sent the
real Voyager on its grand tour). The museum piece flies its one honest transfer instead.
(At the endpoints, where gravity IS competitive, the game pays it honestly — the well
climb-out and the tangent insertion.)

## Market texture note
Daily price wobbles (±15%) are independent per good per port (a hashing bug once correlated
them, giving whole ports systemwide bad days — fixed in vS1.6.0). Geometry still dominates:
Pluto tops Earth-sourced goods ~75% of days when it is the far port, but Neptune will
honestly out-bid it some mornings. Markets breathe; check the board.

## The rest of the loop
The familiar fleet came down the well (Hilux to Conestoga, the temperamental T'Khasi Orion,
the Galliot, the Q-Ship Package at 100 mass of hidden guns), with Earth as the full-catalogue
yard and used lots elsewhere. Pirate heat, ransom/jettison/run choices with thrust-based
escape odds, derelicts that mostly carry mass-and-consequences cargo, tightbeam rumors with
distance-scaled expiry — all present. New solar hazards: **coronal mass ejections** cook
living cargo inside ~1.6 AU (press on and lose 40%, or turtle in the drive shadow at −18%
thrust — which mid-deceleration can mean an overshoot; the Argo's shielding halves losses).
26 goods with real provenance: Lunar helium-3, Venusian float-pharma, Martian xenofossils
(contraband), Titan methane that boils off with a 4-day half-life, Neptune diamond hail,
Kuiper relics, and mangos, which do not enjoy proton storms. Water ice is sourced from Luna, Ceres, Ganymede and Titan — nearly free on Earth and the ice moons, precious only on the dry inner rocks, as it should be. Perishables spoil on an ACCELERATING
hazard (Weibull k=2 — ripening is autocatalytic): fine through the 4-day grace, half gone a
day later, 87% of the remainder the day after that, massacre by day three. Boil-off goods
keep their constant-rate half-lives, because that one really is physics.

## Mid-flight reroutes (with all your inertia)
Catch a tightbeam rumor in transit and the nav computer offers to reroute you on the spot —
to the rumor port, the best current price for the good, or the nearest stocked source. The
solve is honest: your velocity vector is decomposed onto the new chord; the useful component
is kept as a running start, and the sideways component costs a LATERAL KILL burn of exactly
v_perp/a — during which the ship does NOT stop: it coasts on, drifting w·t along the new
chord and v_perp²/2a down its old heading, tracing a sweeping quarter-AU arc onto the new
course (drawn as such). A contrary component gets braked bang-bang — or, if it cannot be braked in
time, overshot and doubled back, as physics demands. Reroute home from a 5,900 km/s Mars
run and you will feel every meter per second of it.

Rumors themselves now STACK in a ledger (ported from the interstellar game, which grew one
while nobody was looking): multiple rumors stay live with independent expiries — no more
new gossip knocking out old — browsable from port via the RUMORS button, each card showing
the paying port, multiplier, expiry, your holdings, the cheapest stocked source, and
one-click intercept plotting.

## Ported from the interstellar frontier (v1.10.x line)
Bulk sales now FLOOD markets: each port absorbs only its natural daily depth at full price
(more near the source); dump more and revenue decays logarithmically, with the log noting
your true average. The captain's log color-codes rumor entries. And Pluto mints
"It's Still A Planet" commemorative plates — their entire value is that almost nobody has
one, so demand halves per plate already sold in a given market, and the game will warn you
before you ruin a perfectly good novelty. Sell one per port, like a person of taste.

## The map
Three.js renders the whole system: real orbits (radially compressed for legibility — the
math underneath is uncompressed), moons on exaggerated display offsets, Saturn's ring, an Earth painted with its actual continents and spun to true Greenwich Mean Sidereal Time — at UTC noon, Greenwich faces the Sun (axis untilted: clock-accurate in longitude, not season-accurate in lighting) —
drag-to-orbit camera opening centered on your current port, click a planet to solve an
intercept and see the plotted chord. Bodies are drawn cartoon-large for legibility from
afar, then shrink toward true scale — with apparent size capped, in transit, at what the body will subtend at the leg's CLOSEST PASS, so nothing ever visibly shrinks: it simply stops growing until true scale catches up — so Jupiter looms on approach
to Ganymede and then resolves to its honest size instead of swallowing your flight path.
Trajectories land tangent on the TRUE limb. Short distances read in light-seconds (Earth–Luna: 1.28 ls), overshoots past 60 ls
escalate to light-minutes, long hauls in AU.
Transit follows the ship POV — the camera rides along, drag-orbits around your hull, planets wheeling past: a tiny detailed torch ship (spine, command sphere, cargo clamps, glowing radiators, flickering drive plume) crawls its trajectory with the camera riding close alongside. Trajectories are drawn in
display space between the displayed bodies: the ship departs from the origin's sphere
surface, peels away tangentially, and lands tangent on the destination's limb (a smoothstep
lateral offset whose zero end-slope makes arrival velocity exactly perpendicular to the
radius — the tangent kiss you were promised, now visible). Overshoots sail past the limb
and double back rather than diving through the core, planets keep
moving, the destination sweeps into the arrival point as you brake — and the HUD narrates
well climb, flip, tangent insertion, and any overshoots you've earned.

Verified headlessly: 37 assertions covering ephemeris sanity, the 3600-second calibration,
intercept convergence, well terms, insertion delicacy thresholds, closed-form overshoot
replans, per-day perishables, and the full economy loop.

Sister game to Interstellar Trail. Based on [the Silk Road](https://krisfricke.github.io/Silk-Road/) by Kris Fricke, an homage to the
classic Oregon Trail.
