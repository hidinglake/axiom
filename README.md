# Axiom

Axiom trains two things that work together whenever you listen, read or think while something else wants your attention: **working memory** (WM, the capacity that test batteries report as a working memory index, WMI) and **selective attention** (SeA).

It is not a memorization drill. A segment asks you to take in a sentence about an idea, keep hold of what it says while your attention is pulled away twice, and then say it back in whatever words you have. The grade answers one question: **what of the idea did you hold?** It does not ask whether you reproduced the sentence.

Everything is in `index.html`. The other files are content the page loads. There is no server and no API behind it.

## A segment, and what each part asks of you

| Part | What happens | What it trains |
| --- | --- | --- |
| **Memorize** | A root phrase stays on screen for the memorization window you set. Above it, images from the categories you chose keep changing. | Working memory: reading for the idea and choosing what to keep. Selective attention: the images are irrelevant, changing and chosen to be hard to ignore. |
| **Spheres** | A 9 by 5 grid of spheres in two close colors. Select every sphere of the less common color. | Selective attention: finding targets among near-identical neighbors. Working memory: the phrase has to survive a task that leaves no room to rehearse it. |
| **Recall** | Write the phrase back. | Working memory: rebuilding the idea from what was kept. |
| **Review** | The root phrase with each cue marked held or lost, your phrase, and the counts. Nothing moves on until you press Start next segment. | Feedback on which kind of thing you tend to drop: names, things, their details. |

The two levels pull on different ends of the same loop. The working-memory level sets how much there is to hold (the length of the phrase). The selective-attention level sets how hard the pull away from it is (how fast the images change, how many odd spheres there are, how close the two colors are). The recall is graded after both pulls, so the score is a measure of what was protected, not of what was seen.

## How a recall is graded

### The idea is held by its cues

When you carry a sentence in your head for a minute, you are not carrying a string of words. You are carrying a few anchors and how they fit: who or what it was about, the things it spoke of, and what it said those were like. Axiom calls these the **cues** of a phrase and grades the recall on them.

| Kind of cue | What it is | Weight |
| --- | --- | --- |
| **Name** | The person, text, place or people the phrase names: *Hobbes*, *Leviathan*, *Athens* | 2 |
| **Noun** | The things the phrase speaks of: *people*, *government*, *fear* | 1.5 |
| **Detail** | What the phrase says a cue is like: *constant* fear, a *single* executive. Counts only when the cue it describes was held too | 0.5 |
| **Verb** | What the cues do to each other: *live*, *protect*, *divide* | 0.25 |
| Order and sentence structure | Where the cues stood and how the sentence was built | not graded |

The score from the cues is the weight of the cues you held divided by the weight of all the cues in the phrase.

Across the 600 root phrases, names carry about 27% of the weight, nouns 58%, and details and verbs about 7.5% each. A level 1 phrase has about 6 cues and a level 10 phrase about 15.

### Why the weights fall this way

- **Names weigh most** because they are the part of an idea that cannot be worked out again. If you lose "Hobbes" you cannot reason your way back to him, and an idea you cannot attribute is hard to use in a conversation.
- **Nouns come next** because they are what the sentence is about. Hold *people*, *government* and *fear* and most of the claim can be rebuilt.
- **A detail is worth something only on its noun.** "Constant" by itself is a word you kept. "Constant fear" is something you understood. A detail recalled without the cue it describes is shown on the review but earns nothing, because the binding is the thing being trained.
- **Verbs weigh least** because how the cues were strung together is the part of a sentence memory keeps worst and needs least. They still count, as a small reward for holding the relation as well as the things related.
- **Order is not graded at all.** Saying the same thing in a different order is not forgetting.

### What the grade makes you practice

A score shapes the strategy people use to earn it. If Axiom graded wording, the way to win would be to repeat the string of words under your breath until the box appeared, which is rote rehearsal, and it is exactly what the spheres are there to break. Grading the cues rewards a different habit, the one that survives distraction and the one a conversation needs: read for the idea, pick out who and what it is about, attach what is said of them, and let the wording go.

That is also where the two skills meet. Selective attention decides what gets in while the images change, and keeps the spheres from pushing it out. Working memory holds the handful of things that got in, bound to their details. The comprehension score is taken at the end of both, so it reports the two together: how much of the idea was selected, bound and protected.

### What counts as holding a cue

A cue is held when the recall has it anywhere, in any form.

- **Any form of the word.** *Fear* is found in *feared*, *fears* and *fearful*; *moral* in *morals* and *morality*; *free* in *freedom*; *death* in *died* and *dying*; *child* in *children*. The page uses the Porter stemmer, a list of families that no rule connects, and a short list of endings (*clear* and *clearer*, *rule* and *ruler*).
- **Any word the phrase's file allows.** Each cue can list other words that mean the same thing in that sentence: *government* is also held by *state*, *fear* by *afraid* or *terror*.
- **A slip of the keys.** One wrong letter is forgiven in a word of five letters or more, two in a word of eight or more.
- **Verbs of saying are one verb.** *Argued*, *held*, *wrote*, *said*, *taught*, *observed* and the like all stand for each other, since "Hobbes argued" and "Hobbes wrote" hold the same thing.
- **A name of several words** needs all its main words (*Art of War* needs *art* and *war*), unless its file lets one stand for it (*Marcus Aurelius* is held by either word).

### One phrase, six recalls

```
Hobbes thought people without government would live in constant fear.
cues:  Hobbes (name, 2) · thought (verb, 0.25) · people (noun, 1.5) · government (noun, 1.5)
       live (verb, 0.25) · constant (detail of fear, 0.5) · fear (noun, 1.5)          total 7.5
```

| Recall | Held | From the cues | Wording accuracy |
| --- | --- | --- | --- |
| Hobbes wrote that with no state, people would always be afraid. | everything but *live* and *constant* | 6.75 of 7.5 = **90%** | 25% |
| Fear, constant fear, is what people live in without government, thought Hobbes. | everything | **100%** | 44% |
| Hobbes thought people without government would live in constant chaos. | *fear* is lost, and *constant* with it | 5.5 of 7.5 = **73%** | 87% |
| hobbes people government fear | the name and the nouns | 6.5 of 7.5 = **87%** | 37% |
| People without rulers live in terror. | *people*, *live*, *fear* | 3.25 of 7.5 = **43%** | 37% |
| Locke thought people need government to protect property. | *thought*, *people*, *government* | 3.25 of 7.5 = **43%** | 29% |

The first and third rows are the point of the design. The first recall shares a quarter of its wording with the root phrase and holds nearly all of the idea. The third copies the sentence almost word for word and loses what it was about.

### The meaning model

A cue list can only know the words it was given. A recall that says the right thing in words the list did not foresee would be marked down unfairly, so a small sentence model (all-MiniLM-L6-v2, about 23 MB, loaded in the background from public CDNs and kept in the browser's cache) also compares the recall with the root phrase as whole sentences.

It can only add, and only a little. It makes up at most three tenths of what the cues missed:

**comprehension** = share of the cues held + 0.3 × the rest × the meaning match

So a recall that held 60% of the cues and matches the meaning fully scores 72%, and full marks always need every cue. The match itself is read strictly: the model's similarity has to pass 0.5 before it counts for anything and reach 0.9 to count in full, because two sentences on the same subject score well above zero even when they say different things. If the model cannot load (offline, blocked, too slow), recalls are graded on the cues alone and the review says the meaning match was not available.

**Phrase recall comprehension** is the score shown on the review. It is what the skill scalar and the session average use. It is shown in the color of its band, with the band's name beside it:

| Comprehension | Band | Color |
| --- | --- | --- |
| 0 to 55% | LOW | red |
| 56 to 75% | MID | yellow |
| 76 to 100% | HIGH | green |

The session average at the end is shown the same way.

### Wording accuracy

The review also shows how close the recall was to the exact wording. It is there for reference and moves nothing. Each word of the original is worth 1 point and each punctuation mark 0.4; a word out of sequence earns half; a misspelled word earns the share of its letters that are right; a wrong capital costs 0.2; and the total is divided by the worth of the original or of the recall, whichever is larger. A high comprehension with a low wording accuracy is a good result: it means the idea was held and then said in your own words.

### Reading the review

The root phrase is shown with every cue marked where it stands:

- **bright and bold**: a name or a noun you held
- bright: a detail or a verb you held
- struck through in red: a cue you lost
- yellow: a detail you recalled without the cue it describes
- dim: words that are not cues

Beside it are the counts for each kind (Names 1 of 1, Nouns 2 of 3, and so on), the meaning match and the wording accuracy.

### The grade and the difficulty

Once three recalls have been made at the current difficulty, their average comprehension decides: above 80% both levels go up one, below 60% both go down one, and in between nothing moves. Because the grade is taken after the images and the spheres, moving up means the idea survived that much distraction, and the next segments bring a longer phrase and a harder pull away from it together.

## Why the cues are written into the phrases

Grading meaning in general needs something that reads: a person, or a language model behind an API. Axiom is one static page with no server and no key, so it cannot ask one. It does the next best thing. It trains on a fixed set of root phrases, and **every phrase carries its own answer key**: its cues, the kind of each, which detail belongs to which cue, and the other words that mean the same thing in that sentence.

The judgment about what matters in a sentence was made once, by hand, when the phrase was tagged. All the page has to do at grading time is check, and checking is something a browser can do in a millisecond, offline, with nothing sent anywhere.

What this costs:

- **The set is finite.** 600 phrases, 60 to a level. They will repeat, and a phrase seen many times is partly remembered rather than held. Adding phrases keeps the training honest.
- **A new phrase needs its cues written.** The notation is below. A phrase with no cues is graded on the meaning model alone, or on wording when the model is unavailable.
- **Synonyms are only the ones listed.** The meaning model is the backstop for the rest.

### The notation

Each `reftext_*.txt` holds one phrase to a line: the phrase, a bar, the text it refers to, a bar, the author (left empty if there is none), a bar, and the cues in the order the phrase uses them.

```
Hobbes thought people without government would live in constant fear. | Leviathan | Thomas Hobbes | *Hobbes, Leviathan; ~thought; people; government, state, lawless, anarchy, nature; ~live; [constant] fear, afraid, terror, danger, war
Genesis opens with God making heaven and earth in six days. | Genesis |  | *Genesis, Bible; ~opens; *God; ~making; heaven; earth, world; [six] days, week, 6
```

| Written | Means |
| --- | --- |
| `;` | the end of one cue and the start of the next |
| `*Hobbes` | a name |
| `people` | a noun (anything with no mark) |
| `~live` | a verb |
| `[constant] fear` | a detail, written before the cue it describes |
| `life [solitary] [poor] [short]` | details written after the cue they describe |
| `[first]` alone between semicolons | a detail that counts by itself |
| `fear, afraid, terror` | after a comma, other words that hold the same cue |
| `*Marcus Aurelius, Marcus, Aurelius` | a name of several words that either word will hold |

When you tag a phrase of your own:

- Mark what the sentence is about, and leave out the nouns that only hold it together (a *kind* of, a *pattern* called, in the *end*).
- Put an adjective in brackets beside its noun. Use a detail on its own for an adverb or a description whose noun is not a cue.
- List the words a person might fairly say instead. Verbs of saying need no list.
- A list with no marks in it is read as a list of nouns, so files written the older way still work.

The text and author are shown as a footnote under the phrase while it is memorized and again in the review. They are never part of what has to be recalled. A line that begins with `#` is a note and is never shown.

## What the grading cannot see

- **It checks that the cues are there, not that the claim is right.** "Hobbes thought government makes people live in constant fear" holds every cue of the example above and scores 100%, though it says the opposite. That follows from not grading structure. The meaning model does not correct it, because it can only add.
- **A list of the right names and nouns scores well by itself**, about 85% on an average phrase, since details and verbs carry about 15% of the weight between them. If you want sentences to matter more, raise `detail` and `verb` in `WEIGHT`.
- **A word can hold a cue by accident.** *Wrote* used as a verb of saying will not pass for *writers*, but a recall that happens to use a listed synonym for another reason is credited.
- **The kinds were assigned by hand**, phrase by phrase, and some calls are arguable (is *the dead* a noun or a detail?). Edit the files where you disagree.
- **The meaning model's settings rest on a handful of real recalls.** A similarity of 0.5 or less counts as no match and 0.9 or more as a full match, and the match can add at most three tenths of what the cues missed. They were tightened from looser first values after recalls that had lost most of their nouns were still scoring in the low 70s. They are `boost`, `low` and `high` in `IDEAS` if they need moving again.

## Background, and what is not claimed

The design leans on a few well-established findings. None of them is evidence that Axiom works; they are the reasons it is built the way it is.

- **Hold something while doing something else.** Daneman and Carpenter (1980) introduced the reading span task, in which people process sentences while holding words, and showed that this kind of measure tracks comprehension far better than a plain word span. A segment has the same shape: storage with an attention-demanding task in the middle.
- **Meaning outlasts wording.** Sachs (1967) found that after a short stretch of intervening speech, listeners could barely tell that a sentence's form had changed but still noticed reliably when its meaning had. Fuzzy-trace theory (Reyna and Brainerd, 1995) describes the same split as verbatim and gist traces. Grading wording grades the trace that fades. Axiom grades the one comprehension keeps.
- **Ideas have parts.** Kintsch and van Dijk (1978) modeled the meaning of a text as propositions, each a predicate with its arguments, and scored recall by the propositions recalled. Axiom's cue list is a simpler cousin: the arguments (names and nouns) and their modifiers (details) carry the weight, and the predicates (verbs) carry little. That weighting is this tool's choice, not a research finding.
- **A feature belongs to its object.** Working-memory models give a central role to binding, the joining of separate pieces into one unit (Baddeley, 2000). Crediting a detail only with its cue is how the grade asks for the bound unit instead of its loose parts.
- **Distraction with a pull.** Schweizer and colleagues (2011, 2013) trained working memory with emotional material and reported gains in control over emotional distraction. The image categories are Axiom's way of making the thing you must ignore worth looking at.

What is not claimed: that practice here raises a WMI score, intelligence or any untrained skill. A meta-analysis of working-memory training (Melby-Lervåg, Redick and Hulme, 2016) found reliable gains on working-memory tasks close to the ones trained and no convincing gains on distant ones. Axiom's bet is the narrow one. It makes the practiced task as close as it can to the thing wanted: holding the cues of an idea you have just taken in, through distraction, well enough to say it back.

References

- Baddeley, A. (2000). The episodic buffer: a new component of working memory? *Trends in Cognitive Sciences*, 4(11), 417-423.
- Daneman, M., and Carpenter, P. A. (1980). Individual differences in working memory and reading. *Journal of Verbal Learning and Verbal Behavior*, 19, 450-466.
- Kintsch, W., and van Dijk, T. A. (1978). Toward a model of text comprehension and production. *Psychological Review*, 85(5), 363-394.
- Melby-Lervåg, M., Redick, T. S., and Hulme, C. (2016). Working memory training does not improve performance on measures of intelligence or other measures of "far transfer". *Perspectives on Psychological Science*, 11(4), 512-534.
- Reyna, V. F., and Brainerd, C. J. (1995). Fuzzy-trace theory: an interim synthesis. *Learning and Individual Differences*, 7(1), 1-75.
- Sachs, J. S. (1967). Recognition memory for syntactic and semantic aspects of connected discourse. *Perception and Psychophysics*, 2(9), 437-442.
- Schweizer, S., Hampshire, A., and Dalgleish, T. (2011). Extending brain-training to the affective domain. *PLoS ONE*, 6(9), e24372.
- Schweizer, S., Grahn, J., Hampshire, A., Mobbs, D., and Dalgleish, T. (2013). Training the emotional brain: improving affective control through emotional working memory training. *Journal of Neuroscience*, 33(12), 5301-5311.

---

# Running Axiom

## The first screen

- **Memorization window**, in seconds, and **Session duration**, in minutes, side by side at the top, typed straight onto the large numbers. The memorization window is how long each root phrase stays on screen to be memorized.
- **Cute**, **Odd**, **Grim**, **Sexy** and **Funny**, the five round buttons, choose the image categories. Any number from one to five can be on at once; the last one on cannot be switched off. The categories decide which folders the images come from and nothing else.
- **Selective attention** and **Working memory**, each 1 to 10, set the difficulty the session starts at.
- **Images during phrase recall** keeps the image window changing above the text box while the phrase is typed. It is off unless switched on.

All of it is remembered from one visit to the next.

While the phrase is memorized, a bar under the image window drains and the seconds left are counted down beside it. Through the whole session the foot of the screen shows the levels in force and, beside them, the session timer. A session ends with three averages: phrase recall comprehension, phrase recall time and sphere time.

## Folder layout

```
index.html
reftext_one.txt … reftext_ten.txt      root phrases for working-memory levels 1 to 10
cute/  odd/  grim/  sexy/  funny/      images for each category
```

Each category's images go in the folder of its name. **Grim** covers violent, gory, gross and frightening images alike; it replaces the earlier Gross, Violent and Scary categories, and a first screen that had any of those on now has Grim on. A category whose folder is missing or empty is left out of the session, and the first screen says so.

## Updating the content

Nothing has to be rebuilt or listed anywhere. The page reads these files fresh each time a session starts, so a change is live once GitHub has republished the site, usually within a minute or two of the commit.

- **Images:** open the category's folder on GitHub, choose Add file, then Upload files, and commit. Delete a file there to retire it. To start a new folder, drag the folder itself onto the upload page at the top level of the repo.
- **Root phrases:** open the `reftext_*.txt` file of the level, edit it, and commit. Each file says at its top how many words its phrases must have and how its cues are written.

`index.html` only needs to change when the trainer itself changes.

## The levels

| Level | New image every | Odd spheres of 45 | Color gap | Phrase length |
| --- | --- | --- | --- | --- |
| 1 | 2.4 s | 7 or 8 | 0.07 | 10 to 11 words |
| 2 | 2.1 s | 8 or 9 | 0.063 | 12 to 13 words |
| 3 | 1.8 s | 9 or 10 | 0.057 | 14 to 15 words |
| 4 | 1.5 s | 10 or 11 | 0.051 | 16 to 17 words |
| 5 | 1.3 s | 11 or 12 | 0.046 | 18 to 20 words |
| 6 | 1.1 s | 12 or 13 | 0.041 | 21 to 23 words |
| 7 | 0.95 s | 13 or 14 | 0.037 | 24 to 26 words |
| 8 | 0.8 s | 14 or 15 | 0.033 | 27 to 29 words |
| 9 | 0.7 s | 15 or 16 | 0.03 | 30 to 33 words |
| 10 | 0.6 s | 16 or 17 | 0.027 | 34 to 37 words |

The image, sphere and color columns follow the selective-attention level, and the phrase length follows the working-memory level. The color gap is how far apart the two sphere colors are; smaller is harder, and about 0.02 is the least an eye can pick out.

The time to memorize is not tied to the levels. You set it in the Memorization window box on the first screen, in seconds (1 to 300, 15 to begin with), and it holds for every segment of the session.

The numbers behind all of this sit together near the top of the script in `index.html`:

| Name | Holds |
| --- | --- |
| `SEA`, `WM`, `MEMO` | the level tables and the memorization window |
| `SKILL` | the skill scalar: how many recalls, and the two thresholds |
| `WEIGHT` | what a name, a noun, a detail and a verb are worth |
| `IDEAS` | how much the meaning model can add, and its two thresholds |
| `BANDS` | where MID and HIGH begin |
| `FAMILIES`, `ENDINGS`, `REPORT` | word families, the endings that join two forms of a word, and the verbs of saying |
| `SCORE` | the weights behind wording accuracy |

## The skill scalar

Difficulty follows the recalls. Once three recalls have been made at the current difficulty, the average comprehension of the latest three decides:

- above 80%, both levels go up one;
- below 60%, both levels go down one;
- from 60% to 80%, nothing moves.

After a move the count starts again, so each difficulty is judged on three recalls made at that difficulty. A level already at 1 or 10 stays there while the other moves. When the difficulty moves, the review says so and gives the two new levels, the foot of the screen shows them from then on, and the next segment is played at them. At the end of a session the first screen stands at the levels the session reached, so the next session starts from there.

## Session time

The session duration counts only time spent inside segments. The session timer at the foot of the screen runs while a segment is played. While a review is read it stands still and is marked as paused, so reading a review does not shorten the session. When the time is used up, the segment in progress is still finished, the timer shows 00:00, and the button on its review reads View session results.

## Adding images

Upload image files (jpg, png, webp, gif, avif, svg) straight into `cute/`, `odd/`, `grim/`, `sexy/` or `funny/`, not into folders inside them. Each image is scaled and cropped from the center to fill the square window.

- File names can be anything, except that a name must not begin with an underscore or a dot: GitHub Pages does not publish those files.
- Keep each folder to 1,000 images or fewer. GitHub lists no more than that for one folder.
- Keep the files small. The window is never wider than 560 px, so about 1,100 px on the shorter side is plenty, and a published site may not exceed 1 GB in all.
- Upload a batch in one commit. Every commit republishes the site.
- The repository is public, so anything in these folders can be seen and downloaded by anyone.

Which image comes next is a random draw from all the images of the chosen categories pooled together, every image as likely as any other, so a category with more images comes up more often. The one limit is on repeats: an image never follows itself, and in a folder with images to spare none comes back within four changes. Images are loaded a few ahead of the window, so a large folder costs no more than a small one.

On GitHub Pages the page asks the GitHub API what is in the folder, so there is no list to maintain. Folder names are matched there without regard to capitals, so `Cute/` is found as well as `cute/`; on any other host the names must be lowercase. The repository must be public for that to work. GitHub allows each visitor 60 such requests an hour, about 30 session starts; past that the page reuses the last list it saw.

If you host somewhere other than GitHub Pages, put a `manifest.json` in each image folder listing its files:

```json
["first.jpg", "second.png"]
```

## The root phrases

The ten files hold 600 phrases, 60 to a level: 15 each on philosophy, ideology, religion and human nature, all within the level's range of words. Each one states an idea from a well-known text in plain words and names the text or its author. They are descriptions written for this trainer, not quotations. Each carries its cues, written as described under The notation above.

The page uses the phrases whose length is in the level's range, and passes over any that are not: a phrase edited to one word too many simply stops appearing. Words are counted as they are typed, so a hyphenated pair counts as two. If a file has fewer than eight phrases in range, the eight nearest in length are used instead and the first screen says so. A file can also be ordinary prose; the page splits it into sentences and, since prose has no cues, grades it on meaning.

The page carries a copy of 80 of these phrases for the one case where a text file cannot be read. That copy does not follow edits to the files.

If the page cannot find its images or read its text, the first screen says so under Start.

## Trying it before uploading

Double-clicking `index.html` in this folder works, with one limit: a browser will not let a page opened as a file read the folders beside it. The three practice images still show, because the page knows their names, but images you add will not, and the phrases come from the set of 80 built into the page. To test your own images and text locally, serve the folder instead:

```
python3 -m http.server 8000
```

Then open http://localhost:8000.
