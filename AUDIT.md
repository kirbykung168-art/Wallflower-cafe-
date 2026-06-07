# Wallflowers Cafe site — audit log

Each change links to the source URL that prompted it. Sources cross-checked against original article text (verbatim quote in the HTML comment beside the change).

## Menu corrections

- **Le Boissom De Kanda → Le Boisson de Kanda** (3 places: meta description, brand-brief comment, menu card heading). Daniel Food Diary prints "Boissom" but this is almost certainly the publication's typo — "boisson" is the standard French word for "drink." Lowercase "de" per French convention. Source comment retained noting DFD's original spelling. Source: <https://danielfooddiary.com/2019/11/19/wallflowerscafe/>
- **Le Boisson de Kanda body copy**: "Won the Signature Drink Award 2016 and remains the most-ordered drink on the menu." → "Reported to have won the Signature Drink Award 2016 and to be the most-ordered drink on the menu." DFD doesn't name the award body; hedged the claim.
- **Dark Beer Cake: "Wongnai's #1 member pick" → "The Wongnai member-recommended slice."** Wongnai has no numeric rank — it has a single "member-recommended" (เมนูแนะนำโดยสมาชิก) item; softened. Source: <https://www.wongnai.com/restaurants/301356Nq-wallflowers-cafe/menu>
- **LOUISE: "Bulleit Rye Bourbon" → "Bulleit Rye".** Asia Bars caption prints "Bullet's Rye Bourbon" — both typo and wrong category (Bulleit makes a Rye whiskey, not a Bourbon). Corrected to product-accurate brand name with a source-attribution comment.

## Press-quote corrections

- **Daniel Food Diary headline**: "Hidden & vintage flower-themed cafe with full display of cakes." → **"Hidden & Vintage Flower-Themed Cafe With Full Display Of Cakes."** Title case to match source verbatim. Trimmed " Near Yaowarat Chinatown" tail. Date specified to **19 Nov 2019**. Source: <https://danielfooddiary.com/2019/11/19/wallflowerscafe/>
- **Time Out amber-lighting quote**: "Soft amber lighting throughout, creating a romantic yet relaxing atmosphere." → **"Soft amber lighting is used throughout, creating a romantic yet relaxing atmosphere."** Restored "is used"; trimmed final " at the same time" tail. Attributed to author Kaweewat Siwanartwong. Source: <https://www.timeout.com/bangkok/bars/wallflowers-upstairs>
- **BK Magazine headline**: verified verbatim. Date specified to **12 Nov 2018**. Source: <https://www.bkmagazine.com/bar/wallflowers-upstairs/>
- **Tazzjang Aey (Wongnai)**: verified the English paraphrase tracks the Thai original ("เอาไอเดียการจัดดอกไม้มาทำคาเฟ่ที่อบอวนไปด้วยกลิ่นของดอกไม้"). Date specified to **10 Oct 2024**. Reviewer name spelling verified. Source: <https://www.wongnai.com/reviews/06ad1c18ee774a8ab2197395379f472e>

## Origin-story corrections

- **Brand-brief comment**: Removed invented phrase "second florist outpost" — replaced with the actually-quoted "Casa Lapin's 'second location in the Old Town' (BK Magazine, 8 June 2016)." BK Magazine never used "florist outpost."
- **Manifesto opening copy** ("We started in 2016 as a florist tucked above an old kombucha brewery") rewritten to factually-accurate: "We opened in June 2016 as Oneday Wallflowers, a flower shop tucked into the old Pure Luck kombucha brewery on Soi Nana — Casa Lapin's 'second location in the Old Town.'" The florist was IN the former kombucha brewery's space, not above it.

## Operational corrections

- **Visit-section hours**: Added a small footnote: "Hours per the cafe's Facebook About. Other listings (Wongnai, Time Out) sometimes show longer hours — call ahead or check Linktree for the current week." Kept Cafe 10:00–18:00 and Bar 17:30–00:00 per Kirby's brief (owner-updated FB About is the most authoritative source he had), but acknowledged the published-source variance: Wongnai shows 10:00–23:59, Time Out cafe 11:00–00:00, Time Out bar 17:30 / 18:00–01:00, LINE Official 11:00–00:00.
- **NanNan review date**: "Oct 2024" → "27 Oct 2024" in the brand brief.

## Verified-and-left-as-is

- **Address**: 31-33 Soi Nana, Pom Prap, Pom Prap Sattru Phai, Bangkok 10100. Confirmed at LINE Official, Wongnai (which has a typo of its own — ป้อมปราบศรัตรูพ่าย — that we did not propagate). Romanization "Pom Prap Sattru Phai" matches Time Out.
- **Thai script**: 31-33 ซอย นานา, แขวง ป้อมปราบ, เขต ป้อมปราบศัตรูพ่าย. Verified clean (no mojibake, correct ศัตรู not ศรัตรู).
- **Phone**: +66 94 671 4433 / tel:+66946714433. Verified.
- **Email**: cafe@wallflowersth.com. Verified.
- **IG**: @wallflowerscafe.th. Verified across Wongnai, BK Magazine, Time Out, LINE Official, Linktree.
- **Linktree** link order verified (Food Menu / Coffee Menu / Cake Menu / Drinks bar / Line@ / Where we are).
- **LINE reservation `lin.ee/ME6TMdA`**: verified live; resolves to <https://page.line.me/622oaerd>, displayed as "Wallflowers | LINE Official Account · Cafe' & Bar Upstairs · 6,866 friends". Kept as primary CTA. (Note: Linktree's LINE button is a different URL `lin.ee/Zh3N801` — same account, different short link. Either works; we didn't claim "this is the Linktree LINE link," so kept ME6TMdA per Kirby's original brief.)
- **All four cocktails** (EDEN, NEGRONI, ROSY STRAIGHT BLUSH, LOUISE) — names and ingredient lists verified verbatim against Asia Bars Wallflowers Upstairs feature (2019-12-30).
- **All cafe prices** (Thai Style 150, Americano 150, Thai Tea 150, Latte 130, Tamarind 250, Filter 250, Le Boisson 250, cake from 150) cross-checked across Wongnai + Daniel Food Diary.
- **27 verified Wallflowers photos** in `images/` — Wongnai user uploads on the official page (day mode) and Asia Bars feature shoot (night mode/cocktails). Each `<img>` carries a `<!-- src: URL, verified via X -->` comment.
- **"Wallflowers"** name spelling: no silent corruption to singular "Wallflower" anywhere in the HTML. Verified by grep.

## Outstanding (flagging for Kirby)

- **Hours discrepancy**: kept FB-About hours per Kirby's brief. If you want me to switch to LINE Official's 11:00–00:00 (which is the only other owner-controlled source), say the word.
- **Casa Lapin founder identity**: my earlier research returned two conflicting names. I did not name a founder anywhere on the site — kept the lineage at "Casa Lapin" only. No change needed unless you want one added.
- **DFD spelling "Boissom"**: silently corrected. If you'd prefer the [sic] approach, flip the call.
