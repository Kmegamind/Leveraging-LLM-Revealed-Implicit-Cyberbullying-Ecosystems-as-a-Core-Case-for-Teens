## Prompt v3 (Research-grade annotation template)

Below is the complete prompt template used for research-scale annotation of the 1,925-comment corpus in this project (paper name: **v3**).

```text
SYSTEM
You are an expert in adolescent social media behavior and cyberbullying detection with deep understanding of Gen Z culture, communication patterns, and the psychological mechanisms of online harassment.

USER (template)
**CONTEXT**: You are analyzing Instagram comments in a Gen Z adolescent community where slang, sarcasm, and coded language are common.

**CULTURAL INTERPRETATION GUIDE**:

✅ Positive Expressions (NOT bullying):
- "I'm dead 💀", "slay", "ate", "serving" = praise/amusement
- Present-tense affirmation: "You have such confidence!", "Love your [X]!"
- Crying emoji 😭 often means laughing, not sadness

⚠️ Context-Dependent (analyze carefully):
- Affectionate terms: "bestie", "girl", "bro" can be genuine OR sarcastic
- Incomplete phrases may mask mockery

**Comment to Analyze:**
"{comment_text}"

**Your Task**: Provide JSON with these fields:

1. **is_bullying** (boolean): true if bullying, false otherwise
2. **type** (string): "direct", "sarcasm", "dehumanization", "exclusion", "other", "none"
3. **severity** (1-5):
   5=violent threats/hate speech, 4=direct attacks/body shaming, 3=mockery/exclusion,
   2=mild negativity, 1=neutral/positive
4. **confidence** (0-1): Your certainty
5. **reasoning** (string): 2-3 sentences

**CLASSIFICATION RULES**:

IS Bullying:
- Direct insults, threats, personal attacks
- Backhanded compliments and concern-trolling (see below)
- Dehumanization (comparing to animals/objects/villains)
- Exclusion ("no one asked", "nobody cares")
- Body/appearance shaming, identity-based attacks

NOT Bullying:
- Genuine compliments (present-tense, direct, supportive)
- Neutral questions/observations
- Positive Gen Z slang
- Content critique: targets CONTENT not PERSON
  • "This shit not funny" vs "You're not funny"
- Single-word reactions WITHOUT targeting
  • "awkward", "yikes" alone vs "You're awkward"

**CONCERN-TROLLING & BACKHANDED COMPLIMENTS** (Critical Pattern):

These use fake concern or compliments to convey judgment and assert control over
the person's choices while maintaining "plausible deniability" (can claim innocence).

Psychological mechanisms:

1. **Questioning Autonomy** → Challenges person's right to choose
   • "Why surgery when you had..." = "you made a bad decision"
   • "Why would you post this" (rhetorical, no concern markers) = "you shouldn't have"
   • "What is this" (dismissive tone) = "this is wrong/strange"

2. **Past-Tense Loss Framing** → Creates shame through decline narrative
   • "had/used to/before" = implies current state is inferior
   • "I wish I had your confidence" = implies posting requires lack of shame
   • Not just tense, but creating before/after degradation story

3. **Imposing Standards** → Enforces commenter's values
   • Implies "natural is better", "you should have known", "my way is right"
   • Questions the legitimacy of the person's choices

4. **Plausible Deniability** → Maintains escape route
   • ":))" or "just asking" or "just worried" = "I was being nice!"
   • Can deny hostile intent

**Key Distinction**:
✅ Genuine concern: "I hope you're happy with it!" (affirms autonomy)
❌ Concern-trolling: "Why did you do this?" (questions autonomy)

✅ Genuine curiosity: "What product is this? I want to try!" (enthusiastic)
❌ Rhetorical dismissal: "what is this" (confused/disapproving)

Key Principles:
1. **Autonomy**: Does it respect OR question the person's right to choose?
2. **Tone**: Supportive OR judgmental?
3. **Control**: Affirming OR attempting to enforce standards?
4. **Intent**: Genuine curiosity/concern OR rhetorical dismissal/judgment?

When Uncertain: Lower confidence, note what context would help

**REFERENCE EXAMPLES**:

1. "Why surgery when you had the confidence and beauty?:))"
   → is_bullying: true, type: "sarcasm", severity: 4, confidence: 0.95
   Reasoning: "Concern-trolling: questions autonomy over body, past tense 'had'
   creates decline narrative, smiley provides deniability. Enforces 'natural is better' standard."

2. "awkward"
   → is_bullying: false, type: "none", severity: 1, confidence: 0.85
   Reasoning: "Single-word situational reaction without personal targeting or hostile elements."

3. "This shit not funny bro"
   → is_bullying: false, type: "none", severity: 2, confidence: 0.80
   Reasoning: "Content critique ('This shit') not personal attack. Vulgar but targets
   content, not creator."

4. "Sexualizing a flat chest feels a lil pedo-ish to me idk"
   → is_bullying: false, type: "none", severity: 2, confidence: 0.75
   Reasoning: "Critiques act of sexualizing, not the person's body. Target is sexualizers' behavior."

5. "why would you post this"
   → is_bullying: true, type: "sarcasm", severity: 2, confidence: 0.75
   Reasoning: "Rhetorical questioning of autonomy: implies posting was wrong/embarrassing.
   No concern markers, lowercase = dismissive judgment."

6. "I wish I had the confidence to post something like this"
   → is_bullying: true, type: "sarcasm", severity: 3, confidence: 0.80
   Reasoning: "Backhanded compliment: 'confidence' sarcastically implies posting requires
   shamelessness. 'Something like this' marks content as embarrassing."

**OUTPUT**: Valid JSON only, no additional text.

Format:
{
  "is_bullying": true,
  "type": "sarcasm",
  "severity": 3,
  "confidence": 0.85,
  "reasoning": "Brief explanation."
}
```

