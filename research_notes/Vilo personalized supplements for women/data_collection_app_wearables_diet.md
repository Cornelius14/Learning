# Non-lab data collection for Vilo: wearables, phone health stores, CGMs, cycle/hormone data, diet capture, questionnaires, medications, and other signals (as of Nov 2026)

Research-process note for the report writer: these notes rest on about 50 web searches run on 2026-11-20. WebFetch could not reach docs.tryterra.co, tryterra.co or developer.garmin.com from this session (DNS blocked by session network policy), and the shared web-search budget ran out before searches on Omron, Junction's current pricing and Oura/Proov could run. So most facts below come from search-result summaries of the cited pages, not full-page reads. Treat exact numbers (prices, rate limits) as "verify before budgeting". Pricing dates are noted where known.

---

## 1. Wearable and phone data: Apple HealthKit, Google Health Connect, and direct APIs (Oura, WHOOP, Garmin, Fitbit/Google, Samsung, Withings, Ultrahuman, Eight Sleep)

### Takeaway
A women's-health app can get most core signals (sleep stages, resting HR, HRV, steps, respiratory rate, SpO2, and above all nightly skin or wrist temperature deviation plus logged menstrual data) through Apple HealthKit and Android Health Connect at no licensing cost, plus free-but-gated direct cloud APIs from Oura, WHOOP, Withings and Ultrahuman. Late 2026 is an unstable period for vendor access. Garmin has paused all new developer applications since spring 2026. The legacy Fitbit Web API is being shut off (late Oct/early Nov 2026) in favor of the new Google Health API. Samsung retired its old SDK. Oura and WHOOP cap unapproved apps at about 10 users and require users to pay for a membership.

### Cited Findings

**Apple HealthKit (iOS, on-device)**
- HealthKit category types include `menstrualFlow`, `ovulationTestResult` (home ovulation tests), `contraceptive`, `lactation` and `sleepAnalysis`. — [Apple HKCategoryTypeIdentifier docs](https://developer.apple.com/documentation/healthkit/hkcategorytypeidentifier.md)
- Cycle-deviation types such as `irregularMenstrualCycles` are read-only: apps "can request permission to read the samples... but you can't request authorization to share them." — [Apple docs: irregularMenstrualCycles](https://developer.apple.com/documentation/healthkit/hkcategorytypeidentifier/irregularmenstrualcycles.md)
- In the Health app, iPhone users can log cycle factors such as pregnancy, lactation and contraceptive use. — [Apple Cycle Tracking guide](https://support.apple.com/guide/watch/apd26429adf0)
- Apple Watch wrist temperature is used to improve period predictions and give *retrospective* ovulation estimates when the watch is worn to sleep. — [Apple Cycle Tracking guide](https://support.apple.com/guide/watch/apd26429adf0)
- Wrist temperature hardware: Apple Watch Series 8 or later, all Ultra models, and SE 3. It samples every 5 seconds during sleep and needs about 5 nights to set a baseline. — [Apple Support: nightly wrist temperature](https://support.apple.com/en-us/HT213275)
- `.respiratoryRate` and `.appleSleepingWristTemperature` samples are only collected during sleep. If the watch is not worn to bed, no samples are recorded. — [Apple Developer Forums](https://developer.apple.com/forums/thread/764078)
- SensorKit's `SRWristTemperature` (iOS 17+) is a separate, research-gated API, distinct from the HealthKit identifier. — [Apple SensorKit docs](https://developer.apple.com/documentation/sensorkit/srwristtemperature.md)

**Google/Android Health Connect (on-device)**
- Health Connect has a skin temperature data type (peripheral body temperature) "to help indicate sleep quality, reproductive health, and possible illness onset". It needs separate READ and WRITE permissions. — [Android Developers: skin temperature](https://developer.android.com/health-and-fitness/health-connect/features/skin-temperature)
- By default an app can read only 30 days of data before its first permission grant. Older history needs a separate `android.permission.health.READ_HEALTH_DATA_HISTORY` permission. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types)
- `CervicalMucusRecord` sits in the "Cycle Tracking" category (`READ_CERVICAL_MUCUS`). `MenstruationPeriodRecord` uses `READ_MENSTRUATION`, the latter per a third-party tutorial. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types); [ProAndroidDev tutorial](https://proandroiddev.com/exploring-health-connect-pt-2-reading-and-writing-data-eea6514b2bbb)

**Oura (cloud REST API v2)**
- API v2 launched in January 2022 and v1 was discontinued in early 2023. Gen3 and Ring 4 users without an active Oura Membership cannot access their data via the API, and partner apps lose access to those users. — [Oura Support: The Oura API](https://support.ouraring.com/hc/en-us/articles/4415266939155-The-Oura-API)
- Temperature is exposed only as deviation from the user's baseline (`temperature_deviation`, `temperature_trend_deviation`), not as absolute temperature. Oura's computed Cycle Insights (period and ovulation predictions) are in-app only and not exposed via the API, per a 2025–26 community feature request. — [Oura community feature request](https://oura-community.canny.io/feature-requests/p/mensuration-ovulation-data-added-to-oura-api)
- Apps are limited to 10 users until Oura approves them, and users consent per data type. — [Oura Partner Support: The Oura API](https://partnersupport.ouraring.com/hc/en-us/articles/20949682312211-The-Oura-API); [Terra blog on Oura API restrictions](https://tryterra.co/blog/oura-api-ai-apps-access-permissions-commercial-restrictions) (third-party)
- The API is described as free for personal and commercial apps, but the agreement reserves the right to add fees with notice. — [Terra blog](https://tryterra.co/blog/oura-api-ai-apps-access-permissions-commercial-restrictions) (third-party; unverified against Oura)
- The Oura API Agreement bars collecting, using, storing, aggregating or transferring Oura data except as expressly permitted, and requires Oura branding and attribution. — [Oura API Agreement](https://cloud.ouraring.com/legal/api-agreement)
- Reported rate limit: 5,000 requests per 5-minute window per token. Sandbox routes (`/v2/sandbox/usercollection/`) return canned data. — [Lava gateway doc](https://www.lava.so/docs/gateway/providers/oura.md) (third-party)

**WHOOP (cloud REST API)**
- The current API is v2 (July 2025). v1 webhooks stopped being published in Nov 2025. Default rate limits are 100 requests/min and 10,000/day per client (HTTP 429 when exceeded), and limits can be raised on request. — [WHOOP rate limiting docs](https://developer.whoop.com/docs/developing/rate-limiting)
- Scopes reported: read:recovery, read:cycles (WHOOP "cycles" are physiological day cycles, not menstrual cycles), read:workout, read:sleep, read:profile, read:body_measurement. Continuous heart rate is NOT available. Use is free but requires a WHOOP membership and device. — [Terra blog: WHOOP API 2026](https://tryterra.co/blog/whoop-api-data-access-permissions-limitations-2026) (third-party)
- Developers report long waits for approval to lift the 10-user cap. — [WHOOP community thread](https://www.community.whoop.com/t/no-response-on-api-app-approval-to-raise-the-10-user-limit/15246.md?page=2)
- API terms: [WHOOP API Terms of Use](https://developer.whoop.com/api-terms-of-use/)

**Garmin (Connect Developer Program: Health API, Women's Health API)**
- The Women's Health API carries data from Garmin's Menstrual Cycle Tracking and Pregnancy Tracking features. — [Garmin Women's Health API](https://developer.garmin.com/gc-developer-program/womens-health-api/)
- Tiers: Starter (push-only, no historical data, limited users) and Enterprise (push or ping/pull, 1+ month of history, unlimited users). Both include Health, Activity and Women's Health APIs. — [Garmin program overview](https://developer.garmin.com/gc-developer-program/overview)
- **Garmin paused review and approval of all new API access requests in spring 2026 and removed the application form. As of mid-September 2026 it had given no reopening timeline.** Existing integrations keep working. — [the5krunner, Sept 14 2026](https://the5krunner.com/2026/09/14/garmin-developer-api-access-paused/); [Garmin forums](https://forums.garmin.com/apps-software/mobile-apps-web/f/garmin-connect-mobile-andriod/441607/garmin-connect-api-access-paused-for-months-what-are-startups-supposed-to-do)
- Garmin launched a separate personal API (an individual's own data, no approval) in Oct 2026. It is not a route for a consumer app with many users. — [the5krunner, Oct 22 2026](https://the5krunner.com/2026/10/22/garmin-personal-api/)

**Fitbit / Google Health API**
- Support for the legacy Fitbit Web API ends Sept 30, 2026. Google gives two different turn-off dates on versions of its page (Nov 2, 2026 or Oct 30, 2026), after which endpoints return HTTP 410. All integrations must move to the Google Health API with Google OAuth 2.0. — [Google Health API: About](https://developers.google.com/health/about); [Fitbit dev site](https://dev.fitbit.com/build/)
- Users must re-consent, because silent migration is not possible. — [Fitbit community announcement](https://community.fitbit.com/t5/Web-API-Development/Introducing-the-next-phase-of-the-Fitbit-Web-API/m-p/5828051)
- Google says more Health Connect data types will be added to the Google Health API in Q4 2026 and Q1 2027 to reach parity. — [Google Health API: About](https://developers.google.com/health/about)

**Samsung Health**
- The legacy Samsung Health SDK for Android was deprecated July 31, 2025, and partners must migrate to the Samsung Health Data SDK. Read-only access can be built and tested in developer mode without a partner request. Writing needs a partner request. — [Samsung migration guide](https://developer.samsung.com/health/android/migration-guide/overview.html)
- Distributing to the public reportedly still needs partnership approval and registered app info. — [Terra blog on Samsung access](https://tryterra.co/blog/samsung-health-medicare-app-library-developer-access) (third-party; unconfirmed by Samsung)
- Readable types include activity summary, **skin temperature**, sleep, sleep apnea, steps, water intake and user profile, plus heart rate, exercise, nutrition and blood glucose. — [Samsung Health Data SDK overview](https://developer.samsung.com/health/data/overview.html); [Samsung data types](https://developer.samsung.com/health/data/guide/features/data-types.html)

**Withings**
- The Public API is open to developers without a contract via a free Partner Hub account. Scopes are user.info, user.metrics (weight, body composition, BP, temperature), user.activity and user.sleepevents. — [Withings developer reference](https://developer.withings.com/llms.md)
- **From Oct 12, 2026, Withings+ (the paid consumer subscription) is required on the "Start for Free" API plan.** The free self-serve tier stays free beyond 10 users once Withings reviews the app. — [Withings developer reference](https://developer.withings.com/llms.md); [Withings API plans](https://static.withings.com/content/api/plans/plans.html)

**Ultrahuman**
- The partner API is not self-serve. It uses OAuth 2.0 with scopes `ring_data` (sleep, movement, steps, HR, HRV, temperature, VO2 max), `cgm_data` (needs an active M1 CGM patch) and `profile`. Base URL: partner.ultrahuman.com. — [Ultrahuman blog: partnership API](https://www.ultrahuman.com/blog/accessing-the-ultrahuman-partnership-api/)
- Access-token lifetime conflicts: about 1 week per Ultrahuman's blog, about 1 day per a third-party OpenAPI model. — [Ultrahuman blog](https://www.ultrahuman.com/blog/accessing-the-ultrahuman-partnership-api/); contradicted by [apis.io](https://apis.io/apis/ultrahuman/ultrahuman-oauth-api/)
- The partner agreement bars redistributing the API or derived data and requires attribution. — [Ultrahuman API Agreement](https://ultrahumanapp.notion.site/API-Agreement-for-Developers-and-Partners-120755317a9180999ce3edcfc1047f58)

**Eight Sleep**
- Eight Sleep publishes no official public developer API. The endpoints online are unofficial, reverse-engineered and unsupported. — [API Evangelist: Eight Sleep](https://providers.apievangelist.com/providers/eight-sleep/); [apis.io](https://apis.io/providers/eight-sleep/)

### Inferences
- **Recommended architecture:** HealthKit (iOS) and Health Connect (Android) as the base layer, read on-device by Vilo's native app. They are free, cover Apple Watch plus the many apps and rings that write into them (Oura, Withings and others sync to Apple Health), and expose women's-health records (menstrual flow, ovulation tests, contraception, lactation, pregnancy, cervical mucus, BBT/skin temperature). Then add direct cloud APIs only where the phone store is incomplete or delayed (e.g., Oura readiness/temperature deviation, WHOOP recovery).
- **For a supplement formula that changes monthly, real-time streaming is unnecessary.** A daily or weekly batch pull is enough, which keeps any direct integration well inside the WHOOP (10k/day) and Oura (5k per 5 min) rate limits.
- **The most women-specific and decision-relevant wearable signal is nightly temperature deviation** (Apple Watch wrist temperature, Oura finger temperature, Samsung and Health Connect skin temperature). It helps infer cycle phase, ovulatory versus possibly anovulatory cycles, and pregnancy. HRV, RHR, steps and sleep stages are mostly context and engagement signals, not formula drivers (see section 9).
- **Garmin cannot be planned for in late 2026** unless Vilo goes through an aggregator that already holds Garmin approval. Fitbit integrations built before Nov 2026 must be rebuilt on the Google Health API.
- **Membership paywalls (Oura, WHOOP, and Withings+ from Oct 2026) mean a user's data access depends on her paying the device vendor**, so Vilo must handle users dropping out of data feeds when subscriptions lapse.

### Gaps
- I could not open Oura's OpenAPI spec to confirm the full v2 endpoint list in late 2026. Believed but not verified this session: daily_sleep, sleep (with HRV and stages), daily_readiness (temperature deviation), daily_spo2, daily_stress, daily_resilience, heartrate, vO2_max, daily_cardiovascular_age, workout, enhanced_tag. Also unconfirmed whether Oura now exposes cycle/period predictions via API, or Oura membership price.
- Not verified this session: HealthKit has no server-side or cloud REST API (data must be read on-device by a native iOS app with HealthKit entitlement and App Review compliance). Also unverified: the exact iOS version that introduced `appleSleepingWristTemperature` (believed iOS 16), and whether Apple's own retrospective ovulation estimates are readable by third-party apps (believed not; only user-logged ovulation tests and wrist temperature samples are).
- I could not confirm the Health Connect `OvulationTestRecord`, `BasalBodyTemperatureRecord` and `IntermenstrualBleedingRecord` permission names (believed to exist), or the detailed Garmin Women's Health API field list and approval criteria (developer.garmin.com was blocked).
- I found no info on the new Google Health API's women's-health coverage or approval process.

---

## 2. Aggregator APIs (Terra, Junction/Vital, ROOK, Spike, Thryve, Validic): pricing, coverage, and build-vs-buy

### Takeaway
Aggregators turn about 6–10 separate OAuth integrations into one SDK and webhook stream, typically for a $300–$500/month base fee plus about $0.50–$1.00 per connected user per month. They also offer a pragmatic route to Garmin while Garmin's own program is closed. Still, they cannot fix the HealthKit and Health Connect on-device constraint: they ship mobile SDKs for that. Published pricing is sparse and often contradicted, so every number needs a sales quote.

### Cited Findings
- **Terra:** Usage-based credits. The Quick Start plan includes 100,000 credits per month. Each connected user (active authentication) costs 200 credits per month, the first 400 events per authentication are free, and extra events cost 0.5 credits. Overage credits cost $0.005 each from 100k to 1M per month and $0.003 above 1M. — [Terra docs pricing](https://docs.tryterra.co/health-and-fitness-api/pricing); [APIs.io Terra plans](https://apis.io/plans/terra-api/terra-api-plans-pricing/) (third-party)
- Terra's homepage says plans start at $399 per month on annual billing. — [Terra homepage](https://www.tryterra.co/)
- Terra add-ons: Streaming API at $99/month plus usage (an active streaming user is 1,000 credits, about $5), and Health Scores at $499/month. — [Sahha comparison](https://sahha.ai/compare/terra-alternatives/) (competitor source; may be biased)
- A Terra community answer puts a 100–500-user pilot inside the free allowance, and 3,000 users at about 600,000 credits per month. — [Terra community](https://tryterra.co/community/authenticated-user-pricing)
- **Junction (formerly Vital):** Rebranded March 11, 2025 with an $18M Series A led by Creandum. Covers 500+ wearables and devices through one API and is now leading with lab diagnostics. — [TechCrunch](https://techcrunch.com/2025/03/11/junction-an-api-to-link-health-wearables-with-labs-raises-18m)
- A Junction pricing page shows a "Launch" plan at $300/month. — [Junction pricing](https://www.junction.com/pricing); contradicted by [Sahha](https://sahha.ai/compare/junction-alternatives/) (says no pricing published and /pricing returns 404). Unresolved.
- **Thryve** (German-hosted): Start Up €499/month for 500 users, then €0.50 per extra user; €999 per additional 10,000 users; Scale Up from €1,000/month. — [Thryve pricing](https://www.thryve.health/pricing)
- **Spike:** Plans "from $450/month", with unlimited integrations and historical data retrieval included. — [Spike pricing](https://spikeapi.com/pricing). A third party says no per-MAU rates are published and pricing is negotiated. — [APIs.io Spike plans](https://apis.io/plans/spike-api/spike-api-plans-pricing/)
- **ROOK:** Capterra lists "$249 per user per month", which looks implausible for a per-end-user price and is probably a mislabeled base fee. Treat as unverified. — [Capterra ROOK](https://www.capterra.com/p/10016968/ROOK)
- Build-vs-buy analyses from an integration consultancy: — [Momentum: real cost of wearables integration 2025](https://www.themomentum.ai/blog/the-real-cost-of-wearables-integration-in-2025-build-vs-buy-analysis); [Momentum: wearable API vs aggregators](https://www.themomentum.ai/blog/wearable-api-integration-vs-saas-aggregators) (content not retrieved)

### Inferences
- **Terra unit economics (my arithmetic from the cited rates):** 200 credits × $0.005 ≈ **$1.00 per connected user per month** in the 100k–1M credit band, about $0.60 above 1M, plus the $399/month base. At 3,000 connected users that is roughly $2,500/month in credits.
- **Thryve at scale:** about €0.10 per user (€999 per 10k), possibly cheapest per user, but with EU hosting and US-market fit to check.
- **Recommendation:** for an MVP, build HealthKit and Health Connect natively (free, and they cover most women's-health records), then use one aggregator for cloud-only devices (Oura, WHOOP, Garmin, Withings, Ultrahuman, Google Health API). Plan to bring 1–2 high-volume integrations (likely Oura) in-house later if per-user fees matter. Women's-health fields (Garmin Women's Health API, cycle data) are where aggregator data models are least standardized, so check them field by field before buying.

### Gaps
- No verified Validic, ROOK or Junction 2026 price sheets. Validic was not covered by any search result.
- Which aggregators currently hold active Garmin Women's Health API, Oura, WHOOP and Google Health API approvals (and whether they pass through women's-health and cycle fields) was not verified.
- Terra's official pricing page could not be fetched (host blocked), so tier names and base fees for late 2026 are unconfirmed.

---

## 3. Continuous glucose monitors (Dexcom Stelo, Abbott Lingo): data access, user cost, usefulness

### Takeaway
OTC CGMs cost users about $89/month. Neither Stelo nor Lingo has an open self-serve developer API. Data reaches third parties through Apple Health (Lingo writes to Apple Health with a 3-hour delay), named partner integrations, or Dexcom's gated, HIPAA-authorization API. Evidence that CGM data improves outcomes in non-diabetic adults is limited, and glucose data has little direct bearing on micronutrient formulation. It is a low-value, high-friction, high-cost signal for Vilo, except perhaps as an optional add-on for users with PCOS or insulin-resistance concerns.

### Cited Findings
- **Stelo pricing:** $89/month subscription or $99 for a two-sensor pack (about 30 days), HSA/FSA eligible (list price as of Aug 2026). — [MedTech Dive](https://www.medtechdive.com/news/dexcom-prices-first-over-the-counter-glucose-monitor/725310/); [NutriScan 2026 price page](https://nutriscan.app/blog/posts/is-stelo-free-2026-dexcom-stelo-price-6fb70d497c) (low-quality source). One 2026 comparison claims $127–$225/month tiers, which conflicts with all other sources. — [knowledgelib](https://knowledgelib.io/fitness/wearables/continuous-glucose-monitors/2026)
- **Lingo pricing (2026, conflicting):** $54 for a 2-week single-sensor plan, $89 for a 4-week two-sensor plan, or $249 for 6 sensors every 12 weeks. — [NutriScan](https://nutriscan.app/blog/posts/is-lingo-free-2026-abbott-lingo-price-02afb68564); older launch price $49 for 2 weeks. — [Fierce Biotech](https://www.fiercebiotech.com/medtech/over-counter-cgm-market-grows-abbotts-lingo-debut)
- **Lingo data access:** Lingo writes 5-minute glucose values to Apple Health with a 3-hour delay, and reads height, sex, steps, weight and workouts from Apple Health. — [Lingo support](https://support.hellolingo.com/hc/en-us/articles/27954887462290-How-do-I-connect-Lingo-to-Apple-Health)
- Lingo launched on Android on Dec 8, 2025. — [Abbott press release](https://abbott.mediaroom.com/2025-12-08-Abbotts-Lingo-TM-Now-on-Android-TM-,-Expanding-Access-to-Real-Time-Glucose-Data?asPDF=1)
- Named Lingo partnerships: Withings (iOS users route via Apple Health, with a direct API integration announced) and Google's AI health coach. I found no general-purpose Lingo developer API. — [Withings Lingo page](https://wcs.withings.com/us/en/lingo); [AI News](https://www.artificialintelligence-news.com/news/google-ai-health-coach-abbott-glucose-data/)
- **Stelo data access:** Stelo shares data only with "Stelo connected partner" apps the user authorizes. — [Stelo partner FAQ](https://www.stelo.com/support/faqs/partners/why-am-i-not-seeing-my-stelo-glucose-data-in-third-party-stelo-connected-partner-applications); [Stelo Terms](https://www.stelo.com/en-us/legal/terms-of-use)
- The Dexcom developer API does not automatically grant production access. It needs OAuth 2.0 plus HIPAA authorization, and "Limited Access" production apps are capped at 5 authorized users. — [Dexcom developer: Scopes & Access](https://developer.dexcom.com/docs/dexcom/scopes-access)
- Ultrahuman's M1 CGM data is available through its partner API under the `cgm_data` scope. — [Ultrahuman blog](https://www.ultrahuman.com/blog/accessing-the-ultrahuman-partnership-api/)
- **Evidence:** A 2026 systematic review and meta-analysis (Eur J Med Res) suggests CGM in non-diabetic people "may improve mean blood glucose and enhance adherence", but says evidence on accuracy and glycemic variability is limited. — [Eur J Med Res 2026](https://link.springer.com/article/10.1186/s40001-026-03920-0)
- A 2024 Diabetic Medicine review found "a lack of consistent and high-quality evidence" for CGM's usefulness in people without diabetes. — [Oganesova et al. 2024](https://discovery.ucl.ac.uk/id/eprint/10195783/1/Diabetic%20Medicine%20-%202024%20-%20Oganesova%20-%20Innovative%20solution%20or%20cause%20for%20concern%20%20The%20use%20of%20continuous%20glucose%20monitors%20in.pdf)
- A 2025 Sensors systematic review frames CGM-guided lifestyle feedback for cardiovascular prevention in healthy adults as promising but unproven. — [Sensors 2025](https://mdpi.com/1424-8220/25/1/187)

### Inferences
- **For supplement personalization, CGM data could at most inform claims on "metabolic support" ingredients** (e.g., inositol for PCOS, chromium, berberine). The evidence base for adjusting doses from consumer CGM traces is essentially absent.
- At about $89/month, a CGM could cost as much as or more than the supplement itself. Most practical uses would be a one-off 2–4-week "baseline" sensor in an onboarding bundle, or simply reading glucose from HealthKit or Health Connect if the user already wears one.
- Fasting glucose and HbA1c from labs (covered by the lab researcher) are more decision-relevant than CGM curves.

### Gaps
- I did not confirm whether Dexcom's partner program accepts wellness and supplement companies for Stelo data, or its terms or fees.
- I did not confirm whether Stelo writes to Apple Health or Health Connect, or with what delay (believed to write to Apple Health; unverified this session).
- I found no study linking CGM metrics to micronutrient needs.

---

## 4. Menstrual cycle and hormonal-stage data (cycle logging, BBT, wrist/finger temperature, urine hormone monitors, menopause scales, PCOS, pregnancy, postpartum and breastfeeding stages)

### Takeaway
Cycle phase and life stage are the highest-value women-specific non-lab inputs. They are cheap to collect: self-report onboarding plus HealthKit or Health Connect cycle records plus optional wearable temperature. Wearable temperature reliably confirms ovulation *after the fact* (about 1.2–1.3-day error in Apple and Oura validations). Urine hormone monitors (Mira, Inito) are more precise but have no public developer APIs, so the practical routes are user-logged results, HealthKit `ovulationTestResult`, or PDF and report uploads. The Menopause Rating Scale is free, while the Greene scale and PSST need licensing for commercial use.

### Cited Findings

**Wearable temperature for cycle phase and ovulation**
- **Apple (preprint, 2023, NCT05852951):** 260 participants and 889 cycles, with LH tests as reference. Retrospective ovulation estimate MAE was 1.22 days, with 89.0% of estimates within ±2 days. Next-menses prediction MAE was 1.65 days. — [JMIR Preprints 50821](https://preprints.jmir.org/preprint/50821) (peer-review status unconfirmed)
- **Oura (JMIR 2025, Oura-employed authors):** 1,155 cycles from 964 participants, with LH tests as reference. It detected 96.4% of ovulations with an average error of ±1.26 days, versus ±3.44 days for the calendar method. In irregular cycles the errors were 1.48 days versus 6.63 days. Detection was weaker in short cycles (OR 3.56, P=.008). — [PMC11829181](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11829181/); [Oura blog](https://ouraring.com/blog/oura-ovulation-detection-algorithm-validation-study/)
- **Earlier wrist-sensor study (2018, 136 women):** A sustained 3-day temperature shift was seen in 357 of 437 cycles (82%). — [PMC6265623](https://pmc.ncbi.nlm.nih.gov/articles/PMC6265623)
- **Ava bracelet vs oral BBT (JMIR 2021):** Wrist skin temperature was more sensitive for detecting ovulation (0.62 vs 0.23, P<.001) but had more false positives. — [PMC8238491](https://pmc.ncbi.nlm.nih.gov/articles/PMC8238491)
- Temperature methods identify ovulation retrospectively and cannot prospectively predict the fertile window from temperature alone. — [PMC6265623](https://pmc.ncbi.nlm.nih.gov/articles/PMC6265623)
- Regulatory precedent: Natural Cycles received FDA 510(k) clearance to use Oura temperature data in 2021, and Apple Watch (Series 8+) wrist temperature from Apple Health in Sept 2023. A 2025 clearance allowed OTC and prescription availability, and a sixth clearance (July 27, 2026) covered an updated algorithm. — [Citeline (Oura)](https://medtech.citeline.com/MT145673/Natural-Cycles-Fertility-App-Wins-FDA-Clearance-For-Oura-Ring-Integration); [BioSpace (Apple Watch)](https://www.biospace.com/natural-cycles-receives-fda-clearance-to-integrate-its-birth-control-app-with-data-measured-by-apple-watch); [Contemporary OB/GYN, July 2026](https://www.contemporaryobgyn.net/view/natural-cycles-receives-fda-clearance-for-ai-powered-fertility-algorithm)
- Apple says Cycle Tracking should not be used as birth control. — [Apple Cycle Tracking guide](https://support.apple.com/guide/watch/apd26429adf0)

**Urine hormone monitors**
- **Mira:** Integrated with Oura in Feb 2026, so Mira users see Oura sleep, readiness and temperature next to their hormone results. The integration is managed in Oura's Settings > App Integrations. Mira users can export PDF reports for any period. No Mira developer API was found. — [HIT Consultant, Feb 10 2026](https://hitconsultant.net/2026/02/10/mira-oura-partnership-hormone-tracking-integration/); [Oura support](https://support.ouraring.com/hc/en-us/articles/10705471244947); [Mira app page](https://shop.miracare.com/pages/mira-app)
- **Inito:** Users can export a full cycle as a structured report with charts and exact hormone values. No partner API was found. The homepage showed the reader at $99 (from $149) at search time. Inito publishes a separate "Consumer Health Data Privacy Policy". — [Inito](https://inito.com); [Inito consumer health data privacy policy](https://inito.com/consumer-health-data-privacy-policy)
- Oura publishes a women's-health partner-platforms page, but its content was not retrieved. — [Oura blog: women's health partner platforms](https://ouraring.com/blog/sv/oura-womens-health-partner-platforms/)
- The Garmin Women's Health API carries menstrual and pregnancy tracking data, but Garmin is closed to new applicants (see section 1). — [Garmin](https://developer.garmin.com/gc-developer-program/womens-health-api/); [the5krunner](https://the5krunner.com/2026/09/14/garmin-developer-api-access-paused/)

**Menopause and perimenopause symptom scales**
- **Menopause Rating Scale (MRS):** A 2003 review says researchers can download language versions and use them "without formal permission". — [Heinemann et al., HQLO 2003 (PMC183844)](https://pmc.ncbi.nlm.nih.gov/articles/PMC183844/). Validation papers: [PubMed 11910610](https://pubmed.ncbi.nlm.nih.gov/11910610/), [PubMed 11910611](https://pubmed.ncbi.nlm.nih.gov/11910611/)
- **Greene Climacteric Scale:** Licensed via RWS Life Sciences. Free for academic researchers and $10 per patient for pharma studies. It cannot carry the Greene name if items are changed, though reformatting is allowed. — [RWS Greene FAQ](https://lifesciences.rws.com/greeneclimactericscale/faqs)
- The Australasian Menopause Society's modified Greene symptom score card (2025) allows reproduction by health professionals for clinical practice. Other uses need approval. — [AMS score card 2025](https://menopause.org.au/images/stories/infosheets/docs/AMS_Symptom_score_card_2025.pdf)

**Heavy menstrual bleeding (HMB), the key bridge to iron**
- The SAMANTA questionnaire (validated for HMB) has 86.7% sensitivity and 89.5% specificity. SAMANTA and the HMB-VAS tool have also been evaluated for iron-deficiency screening (COLIBRI study). — [PMC12547405](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12547405/)
- In a Swedish teen cohort, 52% of girls reporting HMB had iron deficiency versus 26% with normal menstruation. — [Lund University](https://www.lunduniversity.lu.se/article/heavy-menstruation-common-among-teenage-girls-questionnaire-reveals-risk-iron-deficiency)
- In young Australian women, ferritin below 30 µg/L was linked to reporting more than 2 days of heavy bleeding (AOR 1.73). — [Monash University](https://www.monash.edu/medicine/sphpm/womenshealth/research/findings/iron-insufficiency-among-young-australian-women)

### Inferences
- **Minimum viable cycle and life-stage capture (onboarding, about 2 minutes):**
  - Current stage: cycling naturally; on hormonal contraception (type); trying to conceive; pregnant (trimester); postpartum (weeks); breastfeeding; perimenopause; postmenopause; on MHT/HRT.
  - Known diagnoses: PCOS, endometriosis, fibroids, thyroid disease.
  - Period regularity and length.
  - Bleeding heaviness, using a SAMANTA-style short screen.
  - Then sync HealthKit or Health Connect menstrual records, and optionally wearable temperature.
- **Stage drives formula far more than phase.** Pregnancy, trying to conceive, lactation, postmenopause and hormonal contraception each change folate, iodine, choline, iron, vitamin D, calcium and B6 targets and safety limits (e.g., vitamin A form during pregnancy). A monthly formula cannot track within-cycle phases (follicular vs luteal) anyway, so phase data is mostly useful for symptom correlation (PMS) and engagement, not dosing.
- **Confirmed anovulatory cycles** (no temperature shift across several cycles) or very irregular cycles could prompt a "talk to a clinician / consider PCOS evaluation" flag rather than a formula change.
- **For urine hormone monitors, the pragmatic path is reading HealthKit `ovulationTestResult` where the monitor's app writes it, plus manual entry.** Partnership talks with Mira or Inito would be needed for anything richer.

### Gaps
- I could not verify the 2026 Oura × Proov integration, the Clearblue Connected data-export or HealthKit-write behavior, or whether Mira or Inito write to HealthKit or Health Connect.
- I found no independent (non-company) validation of Oura's ovulation algorithm, and the Apple study's peer-review status is unconfirmed.
- Wearable-temperature performance in perimenopause, PCOS and postpartum was not researched (search budget exhausted).
- The MRS's current commercial licensing holder and terms after 2003 are unconfirmed.
- I found nothing on validated PCOS symptom questionnaires (e.g., PCOSQ licensing) or postpartum and breastfeeding-specific nutrient questionnaires.

---

## 5. Diet capture: photo AI APIs, barcode and nutrient databases, accuracy for micronutrients, short FFQs and screeners, pricing

### Takeaway
Photo-based AI food logging is now cheap (Passio about $0.01–$0.63 per active user per month on token pricing). It is validated mainly for energy and macronutrients and only weakly for protein and fat. **I found no solid validation for estimating micronutrients from photos**, and logging adherence collapses within weeks. For supplement personalization, a short validated screener at onboarding, refreshed quarterly (e.g., the free 19-item NCI Dietary Screener Questionnaire, plus targeted iron, calcium and vitamin D FFQ items and diet-pattern questions such as vegan, dairy-free or fish intake), is likely higher value per minute of user effort than continuous photo logging.

### Cited Findings

**Photo and AI logging vendors and pricing**
- **Passio Nutrition AI:** Starter $99/month (1M tokens), Growth $599/month (5M), Pro $2,999/month (100M). Refills cost $25, $10 or $2.50 per 1M tokens respectively. — [Passio platform page](https://www.passio.ai/platform)
- Passio says an active user (logging, scanning, chatting) uses about 250,000 tokens per month. — [Passio token docs](https://passio.gitbook.io/nutrition-ai/getting-started/token-system-and-pricing). Passio marketing also claims 1–10 cents per user. — [Passio cost breakdown](https://www.passio.ai/cost-breakdown). Some Passio pages and third-party listings show different tiers.
- **FatSecret Platform:** The basic tier is free, including commercial use. Pricing depends on the number of country markets, with no per-call volume pricing. Image recognition and NLP are usage-billed add-ons for Premier. — [FatSecret](https://platform.fatsecret.com/); [FatSecret editions](https://platform.fatsecret.com/api-editions); [FatSecret image recognition](https://platform.fatsecret.com/features/image-recognition-and-nlp)
- **Edamam:** The retired Nutrition Data API listed Free, $99/month Basic and $499/month Pro tiers, and a third party cites $49/month. Current pricing was not verified. — [Edamam developer](https://developer.edamam.com/nutrition-data-API); [Medium](https://medium.com/@worldindata/edamam-nutrition-analysis-api-1c8d1c98d5c2)
- **Nutritionix:** A third-party post cites $449/month, and APIs.io describes it as freemium with self-serve signup. — [DEV Community](https://dev.to/raviteja_nekkalapu_/most-nutrition-apis-hide-80-of-the-data-behind-paywalls-mine-doesnt-49pl); [APIs.io](https://apis.io/providers/nutritionix/)
- Comparison page: [GreenChoice API comparison](https://about.greenchoicenow.com/nutrition-data-api-comparison) (not retrieved in full)

**Accuracy evidence (photo and LLM-based)**
- **2023 systematic review:** AI image methods' relative errors for volume and calories "align with, and have potential to exceed" human estimates, but database and reporting heterogeneity prevented meta-analysis. — [PubMed 38060823](https://pubmed.ncbi.nlm.nih.gov/38060823/)
- **3-LLM study (ChatGPT-4o, Claude 3.5 Sonnet, Gemini 1.5 Pro; Curr Dev Nutr, Sept 2025):** Accuracy was comparable to traditional self-report methods, but with systematic underestimation of large portions and high variability in macronutrients. — [PMC12513282](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12513282/)
- **ChatGPT on 114 meal photos (Nutrients, Feb 2025):** Notes that prior LLM work covered only a narrow range of nutrients, and that micronutrients were not considered in earlier text-based work. — [PMC11858203](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11858203/)
- **ChatGPT-5 energy and macros (Nutrients, Nov 2025):** Accuracy fell when visual context was removed. — [PMC12655113](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12655113/)
- **Hospital tray study, 10 AI models vs dietitians (Nutrients 2026):** Protein and lipid accuracy was significantly lower across all models. — [MDPI Nutrients 18(6):966](https://www.mdpi.com/2072-6643/18/6/966/htm)
- **ZOE PREDICT (Proc Nutr Soc, Oct 2025):** Evaluated an LLM photologging system against weighed food logs on real-world meal photos. — [Cambridge Core](https://www.cambridge.org/core/journals/proceedings-of-the-nutrition-society/article/leveraging-imagebased-ai-for-dietary-assessment-evaluating-a-large-language-model-with-realworld-meal-photos-from-the-zoe-predict-cohorts/64BD22D52D629009CED6A8EF65B3E75A)

**Validated short screeners and FFQs**
- **NCI Dietary Screener Questionnaire (DSQ), 19 items:** Covers fruits and vegetables, whole grains, added sugars, dairy, fiber and **calcium**. In NHANES 2009–10 its estimates of mean intake and prevalence agreed closely with two 24-hour recalls. Paper forms, scoring procedures and SAS code are publicly available. — [NCI DSQ evaluation](https://epi.grants.cancer.gov/nhanes/dietscreen/evaluation.html); [NCI screeners](https://epi.grants.cancer.gov/diet/screeners/)
- NCI caveat: screeners are less accurate than 24-hour recalls. They are best for population medians and for ranking individuals as higher or lower intake. — [NCI screeners](https://epi.grants.cancer.gov/diet/screeners/)
- **Calcium, vitamin D and vitamin K FFQ (postmenopausal women, pilot):** 161 items. Correlation with a 5-day diet record was r = 0.63 (Ca), 0.89 (vitamin D) and 0.54 (vitamin K). — [PMC3257701](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3257701/)
- **Vitamin D and calcium semi-quantitative FFQ (Iranian childbearing-age women):** 87 items, with acceptable validity against 24-hour recalls and serum 25(OH)D. — [Frontiers in Nutrition 2022 (PMC9643800)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC9643800/)
- **IRONIC-FFQ (young Polish women):** A brief iron-specific FFQ with satisfactory validity and reproducibility. — [Nutrients 2017 (PMC5372862)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC5372862/)

### Inferences
- **For supplement formulation, diet data matters mostly for a handful of "gap" nutrients:**
  - Iron: red meat, legumes, vegetarian or vegan status.
  - Calcium and vitamin D: dairy and fortified foods.
  - Omega-3: fatty fish servings per week.
  - B12: vegan status.
  - Iodine: dairy, iodized salt, seafood.
  - Folate: leafy greens and fortified grains.
  - Choline: eggs.
  - Fiber.
  
  A 15–25-question targeted screener can capture these "never / weekly / daily" patterns in about 3–5 minutes and is easier to defend than photo-estimated micronutrients.
- **Photo logging could be an optional engagement feature** (e.g., a 3-day "diet snapshot" each quarter) that refines the screener, rather than a required daily task.
- Vilo will likely need a custom composite screener built from validated pieces (DSQ items plus iron and Ca/vit D items). Combining them means the composite itself is unvalidated, which should be disclosed.
- **USDA FoodData Central** is the natural backbone for nutrient composition if Vilo builds its own logging. Vendor APIs mostly layer branded and restaurant foods and image recognition on top.

### Gaps
- I found no validation study quantifying micronutrient (iron, folate, vitamin D, calcium, B12) estimation error from food photos, a key evidence gap. I would expect errors larger than for macronutrients, but this is unverified.
- LogMeal, Calorie Mama and Nutritionix 2026 pricing was not found.
- Not verified this session: USDA FoodData Central is free and public-domain (CC0) via an api.data.gov key with about 1,000 requests/hour. Open Food Facts is a free open barcode database (ODbL).
- No sources this session on DHQ III, Diet ID (image-navigation diet-quality tool) or other brief women-specific micronutrient screeners such as PrimeScreen.

---

## 6. Validated in-app questionnaires (sleep, stress, fatigue, mood, GI, PMS/PMDD, energy, hair/skin/nails): licensing status

### Takeaway
Licensing varies widely. PHQ-9 and GAD-7 are free with no permission needed, as are the NCI DSQ and, per a 2003 statement, the MRS. The PSQI is free only for non-commercial use, and commercial use costs from $1,000/year to $20,000 per study via Pitt. The Greene scale and the PSST need permission or fees. The DRSP is available free through IAPMD's tracker, but its standalone reuse terms are unclear. Mood instruments carry clinical-safety duties (PHQ-9 item 9 asks about suicidal thoughts) that a supplement app must handle with escalation pathways. Their outputs should not drive supplement claims for depression or anxiety.

### Cited Findings
- **PSQI (sleep):** Copyright University of Pittsburgh. Free for non-commercial research and education. Commercial use needs a license: $5,000 per study (small company, 100 or fewer participants), $20,000 per larger study, and internal commercial per-use fees from $1,000/year for fewer than 250 uses. Changes need written permission. — [Pitt Innovation: PSQI](https://inventions.pitt.edu/technologies/pittsburgh-sleep-quality-index--02140); [Pitt Sleep Medicine: PSQI](https://www.sleep.pitt.edu/psqi)
- **PHQ-9 and GAD-7 (mood/anxiety):** "No permission required to reproduce, translate, display or distribute." The official repository is phqscreeners.com. — [psytools SOURCES](https://cdn.jsdelivr.net/npm/psytools@0.6.3/SOURCES.md); [ND HHS PHQ-9/GAD-7 PDF](https://www.hhs.nd.gov/sites/www/files/documents/BH/BHC/PHQ-9-and-GAD-7.pdf)
- **PSST (PMS/PMDD screen):** Copyrighted by McMaster University, with licensing through MILO Business Development. — [McMaster copyright 04-069](https://research.mcmaster.ca/industry-investors/tech/quality-of-life-questionnaires-tools/copyright-04-069/). One validation reported 79% sensitivity and 33.3% specificity, and recommended confirming positives with the DRSP. — [PMC10467366](https://pmc.ncbi.nlm.nih.gov/articles/PMC10467366) (attribution from search summary; verify)
- **DRSP:** PMDD diagnosis requires daily symptom tracking over at least two cycles. IAPMD offers a free tracker built on the DRSP. — [IAPMD symptom tracker](https://www.iapmd.org/symptom-tracker)
- **Menopause scales:** see section 4 (MRS free per 2003; Greene free for academics and $10 per patient for pharma via RWS). — [PMC183844](https://pmc.ncbi.nlm.nih.gov/articles/PMC183844/); [RWS](https://lifesciences.rws.com/greeneclimactericscale/faqs)
- **HMB:** SAMANTA questionnaire, 86.7% sensitivity and 89.5% specificity (licensing not found). — [PMC12547405](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12547405/)

### Inferences
- **A low-cost, defensible questionnaire stack:**
  - PHQ-2/PHQ-9 and GAD-2/GAD-7: free, but use only for wellbeing context and safety routing.
  - A free sleep measure instead of PSQI: an Insomnia Severity Index alternative needs checking, while PROMIS Sleep Disturbance short forms are believed free (see Gaps).
  - MRS for women 40+.
  - DRSP-style daily symptom logging for PMS/PMDD patterns, prompted only in the luteal phase to cut burden.
  - A SAMANTA-style HMB screen.
  - Custom, clearly-labeled-non-validated items for hair, skin, nails and energy.
- **Budget for the PSQI license** if Vilo specifically wants that brand name. Otherwise use free alternatives.
- **Questionnaire value for formula decisions:** HMB screen (high: iron) > life-stage and menopause symptoms (moderate: e.g., calcium/vitamin D emphasis, and possibly ingredients with modest vasomotor evidence) > PMS (low–moderate: calcium and B6 have some PMS evidence, not verified here) > sleep, stress and fatigue scores (low: mostly magnesium or adaptogen "targeting" with weak evidence) > mood (should not drive formulation).

### Gaps
- Not found this session: licensing for PSS-10 (believed free for non-commercial use, with commercial terms unclear), PROMIS (believed free via HealthMeasures, with commercial terms to verify), Fatigue Severity Scale, FACIT-Fatigue (licensed via FACIT.org), GSRS and IBS-SSS (GI), MENQOL, ISI and Epworth.
- I found no validated hair, skin or nail self-report questionnaire suitable for supplement personalization.
- Mapi Research Trust / ePROVIDE pages were not reached.

---

## 7. Medications and conditions intake: capture approach, drug-nutrient interactions, drug database APIs and costs

### Takeaway
Medications are among the highest-value, lowest-friction inputs, because they act mainly as **safety constraints and depletion flags** rather than optimization levers. The free NLM RxNorm/RxNav APIs (no license, 20 requests/sec) handle medication name normalization and autocomplete. Drug–supplement interaction content needs a licensed knowledge base (DrugBank, usage-based commercial license; FDB and Medi-Span quote-only) or a curated in-house rule set for the roughly 20 drug classes that matter.

### Cited Findings
- **RxNorm/RxNav APIs (NLM):** Free of charge. With one exception, no license is needed (the `getProprietaryInformation` function needs a UMLS license). The limit is 20 requests/sec per IP (HTTP 429 above that), and NLM recommends caching results for 12–24 hours. A free UMLS license is needed only to download the full RxNorm releases. — [RxNav Terms of Service](https://lhncbc.nlm.nih.gov/RxNav/TermsofService.html); [RxNorm API](https://lhncbc.nlm.nih.gov/RxNav/APIs/RxNormAPIs.html); [RxNorm terms](https://www.nlm.nih.gov/research/umls/rxnorm/docs/termsofservice.html)
- NLM also offers RxTerms (prescribable name/strength pick-lists) and Prescribable RxNorm APIs. — [RxTerms API](https://lhncbc.nlm.nih.gov/RxNav/APIs/RxTermsAPIs.html); [Prescribable RxNorm](https://lhncbc.nlm.nih.gov/RxNav/APIs/PrescribableAPIs.html)
- **DrugBank:** Commercial use needs a paid license. API access and interaction data come in the commercial tier with usage-based (not per-seat) pricing, and prices are not public. Academic access is non-commercial only. — [DrugBank pricing](https://go.drugbank.com/pricing/); [DrugBank terms of use](https://trust.drugbank.com/drugbank-trust-center/terms-of-use)
- **Oral contraceptives and nutrients:** A 2011 Nutr Rev review found current low-estrogen OCs do not clearly lower folate status and that functional B12 markers were not significantly affected. Earlier depletion findings came from higher-estrogen pills. — [PubMed 21967158](https://pubmed.ncbi.nlm.nih.gov/21967158/)
- A 2013 review lists folic acid, B2, B6, B12, C, E, magnesium, selenium and zinc as nutrients affected by OCs. — [PubMed 23852908](https://pubmed.ncbi.nlm.nih.gov/23852908/). A 1980 review said most studies support OC-related B6 deficiency. — [PubMed 7001015](https://pubmed.ncbi.nlm.nih.gov/7001015/). A 2022 narrative review argues for targeted micronutrient supplementation during COC use. — [PubMed 35856377](https://pubmed.ncbi.nlm.nih.gov/35856377/)
- **Metformin:** Long-term use is associated with B12 deficiency. PPIs and H2 blockers independently affect B12 and magnesium status and compound the metformin effect. — [Diabetes Metab Syndr Obes 2020 (PMC7308123)](https://pmc.ncbi.nlm.nih.gov/articles/PMC7308123)

### Inferences
- **Capture design:**
  - An RxTerms/RxNorm-backed autocomplete for meds, plus checkboxes for common categories so users don't skip them: hormonal contraception (pill, patch, ring, hormonal IUD, implant, injection); thyroid hormone; SSRIs/SNRIs; metformin/GLP-1s; PPIs/H2 blockers; anticoagulants/antiplatelets; MHT/HRT; antiepileptics; isotretinoin/retinoids; spironolactone; lithium.
  - Conditions as a fixed checklist: pregnancy, lactation, PCOS, thyroid disease, celiac/IBD, bariatric surgery, kidney disease, hemochromatosis, bleeding disorders, migraine, anemia history.
  - Re-prompt monthly ("anything changed?").
- **Rule types Vilo needs:**
  - Depletion-driven inclusion: metformin or PPI → B12. PPI → magnesium. OC → possibly B6 or folate, with mixed evidence.
  - Exclusion or caution: anticoagulants → avoid high-dose vitamin K changes, fish oil and vitamin E caution. Pregnancy → vitamin A form and dose limits. Hemochromatosis → no iron. Kidney disease → caution with Mg and K.
  - Timing and separation: thyroid hormone separated from iron and calcium. A once-a-day sachet or pill may be incompatible with levothyroxine users unless timing guidance is given.
- **Drug-database cost:** a curated rule set for about 20 drug classes, maintained by a pharmacist, may be cheaper and more auditable than licensing FDB or Medi-Span for a consumer supplement app.

### Gaps
- Not found: First Databank and Medi-Span pricing (believed quote-only, enterprise-priced), the NIH ODS/NatMed drug–supplement interaction database licensing (believed to be Therapeutic Research Center's NatMed Pro, a paid license), and DrugBank actual price points.
- This session's searches did not cover sources on levothyroxine–calcium/iron absorption, warfarin–vitamin K, SSRI–supplement (e.g., St John's wort, 5-HTP serotonergic risk) or GLP-1 RA nutrient effects. These are well established clinically but not cited here.
- I found no systematic review specific to OCs and magnesium, and the 2015 Shere et al. OC–folate meta-analysis was not retrieved.

---

## 8. Other sources: genetics (23andMe/Ancestry raw data; 23andMe after 2025 bankruptcy), microbiome tests, smart scales and body composition, BP cuffs with APIs

### Takeaway
Raw DTC genetic data can still be uploaded by users: 23andMe remains operational under the nonprofit TTAM Research Institute, and raw-data download still works. But the nutrigenomic evidence for supplement dosing is weak, and genetic data is the most sensitive data class Vilo could hold. DTC gut microbiome tests failed a 2026 reproducibility study, so they should not drive formulation. Smart scales and BP cuffs (Withings via free API, or via HealthKit/Health Connect) give weight and BMI, which matter mainly for vitamin D dosing context and safety, and BP, which matters mainly for safety screening.

### Cited Findings
- **23andMe:** The nonprofit TTAM Research Institute (led by co-founder Anne Wojcicki) acquired 23andMe's Personal Genome Service and research operations, and 23andMe continues to offer DNA testing as a nonprofit. TTAM said it will honor existing deletion and research opt-out policies. — [Yahoo News](https://www.yahoo.com/news/23andme-officially-sold-happen-customers-194104258.html)
- Raw data is still downloadable via Account > Resources > Browse Raw Genotyping Data > Download, after confirming date of birth. — [23andMe Customer Care](https://customercare.23andme.com/hc/en-us/articles/212196868). A 2026 guide says US downloads often take about a week, occasionally up to 30 days. — [Gene Food 2026 guide](https://www.mygenefood.com/blog/how-to-get-your-23andme-raw-data-and-what-to-do-with-it/) (commercial blog)
- Lawmakers and privacy advocates raised concerns that TTAM took ownership without opt-in consent. — [Rep. Schakowsky letter to TTAM](https://schakowsky.house.gov/sites/evo-subsites/schakowsky.house.gov/files/evo-media-document/final-letter-to-ttam-research-institute-on-23andme-proposed-purchase.pdf)
- **Microbiome:** In Servetas et al. (Communications Biology, 2026), identical stool samples sent to 7 DTC companies (3 kits each) gave results whose between-company variation was comparable to biological variation between different people. Repeat tests from the same provider were also inconsistent (one replicate set returned 2 "healthy" and 1 "unhealthy"). Some companies sell their own probiotics and supplements based on the results. — [University of Maryland, Mar 2026](https://www.umaryland.edu/news/archived-news/march-2026/gut-check-study-raises-questions-about-at-home-microbiome-testing.php); [NIST publication](https://www.nist.gov/publications/evaluating-analytical-performance-direct-consumer-gut-microbiome-testing-services); [GenomeWeb](https://www.genomeweb.com/genetic-research/buyer-beware-consumer-marketed-gut-microbiome-test-results-vary-wildly-new-study)
- **Withings** (scales, BP monitors, thermometers, sleep mat): the free Public API scope `user.metrics` covers body measurements. Withings+ is required on the free plan from Oct 12, 2026. — [Withings developer reference](https://developer.withings.com/llms.md)
- Samsung Health Data SDK readable types include blood glucose and others, and body composition/BP types are listed on its data-types page. — [Samsung data types](https://developer.samsung.com/health/data/guide/features/data-types.html)

### Inferences
- **Genetics:**
  - At most, offer an *optional* raw-file upload (23andMe or AncestryDNA .txt) parsed for a few well-characterized variants (e.g., MTHFR C677T for folate form, HFE C282Y/H63D as an iron-safety exclusion flag).
  - Store only the derived flags and delete the raw file. Holding whole genotype files creates breach and state genetic-privacy liabilities that outweigh their value.
  - The HFE flag (avoid iron) is arguably the single most useful genetic data point for an iron-containing women's formula.
- **Microbiome:** given the 2026 reproducibility findings, do not integrate DTC microbiome results into dosing. At most, GI symptom questionnaires can guide whether to include a probiotic or fiber component.
- **Weight and BMI:** worth collecting by self-report or a synced scale for vitamin D needs (higher body weight is associated with lower 25(OH)D response) and pregnancy weight-gain context. Body-fat % adds little.
- **BP:** a safety signal (e.g., caution with licorice or high-dose stimulant botanicals), not a dosing driver.

### Gaps
- AncestryDNA raw-data download status in 2026 was not researched.
- Omron's developer API status was not researched (search budget exhausted). Believed: Omron has a partner-only API, and Omron Connect syncs to Apple Health and Health Connect; unverified.
- Evidence for specific nutrigenomic dosing (MTHFR → methylfolate, VDR, FUT2 → B12) was not researched this session.

---

## 9. Evidence-based value of each signal for supplement personalization, ranked against collection friction

### Takeaway
The strongest non-lab drivers of a women's supplement formula are **life stage** (pregnancy, TTC, lactation, perimenopause/postmenopause), **medications and conditions** (safety exclusions and depletions), **menstrual blood loss** (an iron proxy) and **diet pattern** (vegan/vegetarian, dairy, fish). All are collectible by questionnaire in minutes. Wearable physiology (HRV, RHR, sleep stages, steps, SpO2, VO2 max) has weak or no evidence for changing nutrient doses and is better used for engagement and outcome tracking. Wearable temperature is the one wearable signal with women-specific value (cycle confirmation and life-stage hints), though it changes the formula only indirectly.

### Cited Findings
- **Magnesium and HRV/sleep:**
  - A 6-week RCT of magnesium L-threonate (n=100, poor sleepers) improved Oura-measured HR and HRV (sleeping HR down 1.32 bpm) and some subjective sleep measures, but **not objective sleep**. — [Frontiers in Nutrition 2025 (PMC12832366)](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12832366/)
  - A German RCT of 400 mg/day for 90 days (n=100) reported increased HRV parameters. — [PubMed 27933574](https://pubmed.ncbi.nlm.nih.gov/27933574/)
  - A magnesium bisglycinate RCT (n=155) found modest improvement in insomnia severity. — [PMC12412596](https://pmc.ncbi.nlm.nih.gov/articles/PMC12412596)
  - A 2025 review called for robust RCTs. — [ESMED review](https://esmed.org/?p=34360)
- **Menstrual blood loss and iron:** 52% iron deficiency in teens with HMB versus 26% without. — [Lund University](https://www.lunduniversity.lu.se/article/heavy-menstruation-common-among-teenage-girls-questionnaire-reveals-risk-iron-deficiency). Ferritin below 30 µg/L was linked to more than 2 days of heavy bleeding (AOR 1.73). — [Monash](https://www.monash.edu/medicine/sphpm/womenshealth/research/findings/iron-insufficiency-among-young-australian-women). The SAMANTA HMB screen has 86.7% sensitivity and 89.5% specificity. — [PMC12547405](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12547405/)
- **Medications:** metformin, PPI and H2RA effects on B12 and magnesium. — [PMC7308123](https://pmc.ncbi.nlm.nih.gov/articles/PMC7308123). OC effects on B6, folate and B12 are mixed with modern pills. — [PubMed 21967158](https://pubmed.ncbi.nlm.nih.gov/21967158/); [PubMed 23852908](https://pubmed.ncbi.nlm.nih.gov/23852908/)
- **Wearable temperature** confirms ovulation retrospectively with about 1.2–1.3-day error. — [Oura JMIR 2025](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC11829181/); [Apple preprint](https://preprints.jmir.org/preprint/50821)
- **CGM in non-diabetics:** limited, inconsistent evidence. — [Eur J Med Res 2026](https://link.springer.com/article/10.1186/s40001-026-03920-0); [Oganesova 2024](https://discovery.ucl.ac.uk/id/eprint/10195783/1/Diabetic%20Medicine%20-%202024%20-%20Oganesova%20-%20Innovative%20solution%20or%20cause%20for%20concern%20%20The%20use%20of%20continuous%20glucose%20monitors%20in.pdf)
- **Microbiome DTC tests:** not reproducible. — [UMaryland 2026](https://www.umaryland.edu/news/archived-news/march-2026/gut-check-study-raises-questions-about-at-home-microbiome-testing.php)
- **Photo-based micronutrient estimation:** not validated. Macronutrient accuracy is moderate, and protein and fat are weaker. — [PMC12513282](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC12513282/); [MDPI 2026](https://www.mdpi.com/2072-6643/18/6/966/htm)

### Inferences

**Ranking of non-lab signals: personalization value versus friction.** This is my synthesis from the cited evidence plus standard nutrition practice. Labs (ferritin, 25(OH)D, B12, etc.) are covered elsewhere and would outrank most of these.

| Rank | Signal | How collected | Friction | Personalization value | Why |
|---|---|---|---|---|---|
| 1 | Life stage (pregnant/trimester, TTC, postpartum, lactating, peri/postmenopause, on MHT) | Onboarding Q + monthly check-in; HealthKit pregnancy/lactation/contraceptive records | Very low | **Very high** | Changes folate, iodine, choline, iron, vitamin D, calcium and DHA targets and safety limits (vitamin A) |
| 2 | Medications (OC/HC type, levothyroxine, metformin, PPI, SSRIs, anticoagulants, GLP-1) and conditions (PCOS, thyroid, celiac/IBD, bariatric, kidney, hemochromatosis) | RxNorm autocomplete + checklists | Low | **Very high (safety)** | Exclusions, depletion flags (B12), timing conflicts |
| 3 | Menstrual blood loss (HMB screen, period length/heaviness) | SAMANTA-style Qs; HealthKit/Health Connect flow records | Low | **High** | Strongest non-lab iron-need proxy; ~2× iron-deficiency prevalence with HMB |
| 4 | Diet pattern (vegan/vegetarian, dairy, fish/omega-3, red meat, eggs, fortified foods, iodized salt) | 15–25-item screener (DSQ + targeted items), refreshed quarterly | Low–moderate | **High** | Drives B12, iron, omega-3, calcium, vitamin D, iodine, choline |
| 5 | Sun exposure, skin tone, latitude/season, body weight | Qs + phone location (season) + scale/self-report | Very low | **Moderate–high** | Vitamin D dosing context |
| 6 | Symptom clusters (PMS/PMDD, vasomotor/MRS, fatigue, hair shedding, GI) | Validated or custom Qs; luteal-phase prompts | Moderate | **Moderate** (ingredient selection, outcome tracking) | Evidence for symptom-targeted micronutrients is modest; useful for monitoring response |
| 7 | Cycle phase / ovulation confirmation (wearable temperature, LH tests) | HealthKit/Health Connect/Oura sync; manual LH entry | Low if already wearing device | **Low–moderate** | Mainly life-stage hints (anovulation, perimenopause, pregnancy); a monthly formula can't follow phases |
| 8 | Activity / exercise volume (steps, workouts, VO2 max) | HealthKit/Health Connect/wearable APIs | Very low (passive) | **Low–moderate** | Endurance athletes have higher iron and electrolyte losses, a context flag |
| 9 | Sleep, HRV, RHR, stress scores | Wearables | Very low (passive) | **Low** | Small RCTs only (magnesium); good for outcome tracking, not dosing |
| 10 | CGM glucose | OTC CGM ($89/mo) | High | **Low** | Weak evidence in non-diabetics; little micronutrient link |
| 11 | Photo food logs | Passio/FatSecret etc. | High (adherence decays) | **Low for micronutrients** | No micronutrient validation |
| 12 | DTC genetics | Raw-file upload | Moderate (privacy) | **Low** (except HFE iron-safety flag) | Weak nutrigenomic dosing evidence |
| 13 | DTC microbiome | Kit | High ($, stool) | **Very low** | Results not reproducible |

- **A defensible product posture:** "Questionnaire and life-stage-driven formula, with labs as the precision layer, and wearables as feedback and engagement." Wearable data should be framed as *tracking how you feel or sleep on the formula*, not as what sets the doses.

### Gaps
- I found no published study showing that personalizing a supplement formula from wearable data improves outcomes versus a fixed formula.
- PMS-specific micronutrient evidence (calcium, B6, vitamin D, magnesium) and vasomotor-symptom supplement evidence were not researched this session.
- The table's rank ordering is reasoned synthesis, not derived from a published framework.

---

## 10. User friction and compliance: food logging and questionnaire burden

### Takeaway
Continuous food logging decays fast: fewer than half of trial participants are still tracking after week 10, logging drops from about 6 to about 2 days/week by week 8 in app interventions, and only about 2.6% of users of a free photo-diet app used it actively. Short, intensive protocols (about 8 days) and newer AI-assisted logging hold up better. Vilo should design for one-time or periodic bursts and passive sync rather than daily logging.

### Cited Findings
- In two 6-month weight-loss trials, self-monitoring declined over time and fewer than half of participants were still tracking after week 10. "Days with ≥2 eating occasions logged" was the best adherence metric (it predicted weight loss). — [PubMed 31155473](https://pubmed.ncbi.nlm.nih.gov/31155473/)
- In an 8-week app-delivered intervention, food tracking fell from about 6 days/week in week 1 to about 2 days/week in week 8 (cited in a 2024 trial protocol). — [NCT06311175 protocol](https://cdn.clinicaltrials.gov/large-docs/75/NCT06311175/Prot_000.pdf)
- Across three 8-day image-based food-logging EMA studies, logging declined only slightly (mostly snacks dropping off between day 1 and day 2), and trajectories were "remarkably stable". — [JMIR mHealth 2020 (e15430)](https://mhealth.jmir.org/2020/10/e15430/)
- In a free photo-based dietary app, only 2.58% of users (4,895/189,770) used it actively. — [JMIR 2014 (e109)](https://www.jmir.org/2014/4/e109/)
- In a 21-day study of a multimodal AI food-logging app (n=6), all completed and 4 of 6 logged daily. The authors note longer studies are needed to assess "logging fatigue". — [SnappyMeal, arXiv 2025](https://arxiv.org/pdf/2511.03907)
- PMDD diagnosis by DRSP needs daily tracking across at least 2 cycles, an inherently high-burden protocol. — [IAPMD](https://www.iapmd.org/symptom-tracker)
- Health Connect apps see only 30 days of history unless they request an extra history permission, so passive backfill depends on asking for it. — [Health Connect data types](https://developer.android.com/health-and-fitness/health-connect/data-types)
- OTC CGM costs about $89/month to the user. — [MedTech Dive](https://www.medtechdive.com/news/dexcom-prices-first-over-the-counter-glucose-monitor/725310/)

### Inferences
- **Collection design aligned with these decay curves:**
  - Onboarding of about 8–12 minutes in total: life stage, meds and conditions, HMB screen, a 15–25-item diet screener, and 1–2 symptom scales chosen by life stage.
  - One-tap HealthKit / Health Connect / wearable connect, with history permission requested up front.
  - A monthly 60–90-second "formula check-in" before each shipment: life-stage change, new meds, period heaviness, 3–5 symptom sliders.
  - Optional quarterly 3-day photo-logging "snapshot".
  - Daily symptom logging only for users who opt into PMS/PMDD tracking.
- **The monthly subscription cadence is itself the compliance hook:** tying the check-in to "confirm next month's formula" likely outperforms open-ended logging prompts. This is reasoning, not a sourced finding.
- **Device ownership skews to wealthier users,** so wearable-dependent features will reach only a subset. Questionnaire-based personalization must stand on its own.

### Gaps
- I found no data on completion or drop-off rates for multi-scale health questionnaires in consumer apps (e.g., onboarding abandonment per additional minute), or on the share of US women 20–60 who own a wearable that records temperature.
- I found no published retention data specific to personalized-supplement apps.
- Cycle-data privacy and sensitivity notes (brief, legal analysis covered elsewhere): Inito publishes a separate "Consumer Health Data Privacy Policy" (typical of compliance with state consumer-health-data laws). — [Inito](https://inito.com/consumer-health-data-privacy-policy). Lingo obtains consent for each integration. — [Lingo privacy notice](https://www.hellolingo.com/privacy-notice). Apple requires per-type read/write permission that users can revoke. — [Apple Health privacy](https://apple.com/legal/privacy/data/en/health-app). Vendor API agreements (Oura, Ultrahuman) restrict onward transfer and aggregation of their data. — [Oura API Agreement](https://cloud.ouraring.com/legal/api-agreement); [Ultrahuman API Agreement](https://ultrahumanapp.notion.site/API-Agreement-for-Developers-and-Partners-120755317a9180999ce3edcfc1047f58). The legal implications (HIPAA non-applicability, Washington MHMDA, FTC Health Breach Notification Rule, post-Dobbs reproductive-data risk) were not researched here.
