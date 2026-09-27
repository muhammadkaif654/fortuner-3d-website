# AI video prompts — source footage for the scroll sequences

Three shots, one per cinema section. Each is written to scrub well: one
continuous take, constant camera speed, locked exposure, and no cuts. That's
what makes a frame sequence feel like a real camera move instead of a slideshow.

| # | Section in site | Drop extracted frames into |
|---|-----------------|----------------------------|
| 1 | 02 Design (orbit) | `assets/sequences/hero/` |
| 2 | 04 Terrain | `assets/sequences/offroad/` |
| 3 | 06 Interior | `assets/sequences/cockpit/` |

---

## 1 · Hero 360° orbital turnaround

**Prompt**

> Photorealistic cinematic automotive product film, single continuous take, 8 seconds, 16:9, 24 fps.
> A pearl-white Toyota Fortuner Legender (full-size, body-on-frame, seven-seat SUV) with a gloss-black
> two-tone roof sits perfectly still in the centre of a seamless dark infinity-cove studio. The floor is
> polished black epoxy that shows a crisp, mirror-like reflection of the vehicle.
> The camera makes exactly one smooth, constant-speed 360° orbit around the car at headlamp height
> (about 1.1 m) and a fixed distance. It starts on the driver-side front three-quarter view and finishes
> on that same framing, so the clip loops seamlessly. The car stays centred and the same size in frame the whole time.
> Lighting: three long overhead rectangular softbox strips lay liquid reflections along the hood, roof and
> flanks. A warm amber rim light behind camera-left and a cool blue rim light behind camera-right trace the
> silhouette. The quad-LED headlamps and LED daytime running lights are on with a crisp ice-white glow;
> the LED tail lamps glow red.
> Vehicle details: split chrome grille with the Toyota emblem, slim quad-LED headlamps, a sharp beltline that
> kicks up at the rear quarter window, 18-inch dual-tone machined alloy wheels, black wheel-arch cladding,
> satin-silver front and rear skid plates, dark roof rails.
> The background falls off to pure black with faint atmospheric haze and subtle volumetric light shafts.
> Shot on ARRI Alexa 65, 50 mm lens, f/5.6, whole vehicle tack-sharp, no motion blur, locked exposure and
> white balance. Ultra-detailed reflections, high-end automotive commercial grade.

**Negative prompt**

> people, text, captions, watermark, logo overlay, camera shake, handheld, cuts, zoom, dolly-in, speed ramp,
> lens flare crossing the car, morphing or warping bodywork, changing paint colour, extra wheels, melted or
> misspelled badges, floating car, wet floor puddles.

---

## 2 · Dynamic action / off-road tracking shot

**Prompt**

> Photorealistic cinematic action shot, single continuous take, 8 seconds, 16:9, 24 fps.
> A Toyota Fortuner Legender in Avant-Garde Bronze metallic tears across a golden-hour desert canyon trail
> at speed. The camera is on a stabilised tracking-vehicle arm, low at bumper height, holding an aggressive
> front three-quarter angle and matching the SUV's speed exactly. The vehicle stays locked in the left-centre
> third of the frame for the whole shot while the landscape streams past behind it.
> The suspension compresses and rebounds over sandy ridges, the front wheels articulate, and the tyres throw
> arcs of sand and a billowing dust plume that glows amber in the backlight. Headlamps on.
> Environment: sun low behind jagged red-rock ridgelines, long raking shadows, heat haze, layered mountains
> fading into atmospheric perspective, a few desert shrubs whipping past in the foreground.
> Anamorphic 40 mm lens, 180° shutter: natural motion blur on the background, the vehicle stays crisp.
> Teal-and-amber grade, rich contrast, fine film grain, high-end automotive commercial.

**Sand-dune variant.** Replace the environment line with:

> Rolling Saharan dunes with razor-sharp crests, the SUV cresting a dune and carving down its face, sand
> spraying in a rooster tail, deep blue sky fading to warm haze at the horizon.

**Negative prompt**

> people, text, watermark, camera shake, cuts, whip pans, the vehicle drifting out of frame or changing size,
> morphing bodywork, extra wheels, floating vehicle, wrong-way tyre rotation, cartoonish dust.

---

## 3 · Interior / cockpit fly-through

**Prompt**

> Single continuous shot with no cuts, 8 seconds, 16:9, 24 fps, photorealistic.
> It opens tight on the front of an Attitude Black Toyota Fortuner Legender at night in a dark studio. The split
> chrome grille, the Toyota emblem and the glowing ice-white quad-LED headlamps fill the frame.
> The camera pushes forward smoothly and continuously. It slips between the grille slats in a seamless macro
> transition with a brief bloom of light, glides up over the dark silhouette of the engine bay, passes through
> the windshield glass and enters the cabin, where it settles at the driver's eye point behind the steering wheel.
> Cabin: dark leather dashboard with bronze contrast stitching, soft-touch surfaces, and warm-amber and ice-blue
> ambient light strips along the dash and door panels. A floating touchscreen shows a navigation map, the
> analog instruments have ice-blue needles sweeping upward, and the leather-wrapped three-spoke steering wheel
> has paddle shifters. Right-hand drive.
> Through the windshield: a mountain road at blue hour with a faint warm glow on the horizon.
> Camera motion: constant velocity that eases out gently into the final framing, perfectly stable, no roll.
> Probe-lens macro-to-wide feel, with focus racking from the grille to the cockpit. Moody, high contrast,
> crisp detail, premium automotive commercial.

**Negative prompt**

> people, hands, text, watermark, cuts, cross-dissolves, camera shake, rotating horizon, distorted steering
> wheel, melted dashboard, gibberish on screens, left-hand drive, flickering lights.

---

## Getting consistent, scrub-friendly footage

- **Lock the car's identity first.** Generate or photograph a hero still of the exact car and colour, then use
  image-to-video (first-frame conditioning) in every tool. This keeps the grille, wheels and paint consistent
  between shots.
- **Seamless orbit.** In tools that support first and last keyframes, use the same image for both so shot 1 loops.
- **Constant speed beats drama.** Speed ramps and whip pans look great in a trailer but stutter when scrubbed.
  If a clip has a ramp, trim around it with `--start` / `--duration` in the extractor.
- **Upscale before extracting.** If the generator outputs 720p, upscale to 1080p or higher first (for example
  with Topaz Video or your generator's upscaler), then extract.
- **Brand names.** Some generators block trademarked names or logos. If a prompt is refused, describe the
  vehicle instead ("full-size seven-seat body-on-frame SUV with a split chrome grille and slim quad-LED
  headlamps") and rely on your reference image.

### Per-tool notes

Features and limits change often, so check each tool's current docs.

| Tool | Suggested settings |
|------|--------------------|
| **Google Veo** | 16:9, 8 s clips. Use image-to-video with your reference still. Audio isn't needed; it's discarded during extraction. |
| **Kling** | Professional/high-quality mode, 16:9, 10 s. Image-to-video with a reference; use the orbit camera control for shot 1. |
| **Runway (Gen-3 / Gen-4)** | 16:9, 10 s. Use first/last keyframes for the loop, and camera-control presets for the orbit and the push-in. |

Once you have the clips, go to **README → Step 2** to split them into frames.
