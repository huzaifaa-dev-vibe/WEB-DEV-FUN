# UX

> User experience is everything the user experiences. Not just the UI.

---

## Purpose

Master UX principles, research methods, flows, and patterns that make products usable, useful, and delightful.

## Prerequisites

- [UI/](../UI/) basics.

## Learning Outcome

You can design flows that users complete successfully, conduct user research, and improve UX iteratively.

## Dependencies

- None (anyone can learn UX).

## Related Files

- [UI/](../UI/) · [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/) · [UX/research.md](research.md) · [UX/flows.md](flows.md) · [UX/microinteractions.md](microinteractions.md)

## AI Instructions

When designing UX:
1. **Start with the user's task**, not your features.
2. **Map the flow** before designing screens.
3. **Plan for all states**: empty, loading, error, success, partial.
4. **Reduce friction**: fewer fields, fewer steps, sensible defaults.
5. **Don't hide critical actions** behind mystery menus.
6. **Test with real users** if at all possible.

## Human Notes

UX is not UI. UI is what they see; UX is what they experience. A pretty UI with bad UX is worse than an ugly UI with good UX.

### Core principles
- **Don't make me think** (Krug) — interfaces should be self-evident.
- **Hick's Law** — more choices = slower decisions. Reduce options.
- **Fitts's Law** — bigger + closer = faster. Make primary actions big.
- **Jakob's Law** — users spend most time on other sites. Don't reinvent patterns.
- **Miller's Law** — working memory ~7±2 items. Group.
- **Aesthetic-Usability Effect** — pretty things feel more usable.
- **Doherty Threshold** — response < 400ms feels instant.
- **Parkinson's Law** — work expands to fill time. Tighten flows.
- **Serial Position Effect** — first + last items remembered best. Put important there.

### UX research methods
- **User interviews** — qualitative, exploratory.
- **Surveys** — quantitative.
- **Usability testing** — watch users use the thing.
- **A/B testing** — compare two versions.
- **Card sorting** — information architecture.
- **Tree testing** — validate IA.
- **Heatmaps** — see where users click/scroll.
- **Session replay** — see real sessions.
- **Analytics** — what users do.
- **Feedback widgets** — what users say.

→ [UX/research.md](research.md)

### User flows
Before designing screens, design the flow:
```
Landing → Signup → Onboarding → Dashboard → First Action → Success
```
Map every step, branch, and exit. → [UX/flows.md](flows.md)

### Information architecture
- Group related items.
- Use clear labels (user vocabulary, not internal).
- Shallow > deep (3 clicks rule, mostly myth but spirit true).
- Test with tree testing.

### Onboarding
- Show value before asking for signup.
- Progressive disclosure — don't overwhelm.
- Show one new thing at a time.
- Skip option for power users.
- Track completion.

### Forms (UX)
- One column.
- Top-aligned labels.
- Group related fields.
- Sensible defaults.
- Inline validation (on blur, not on every keystroke).
- Clear error messages.
- Don't punish valid input (no "must be 8 chars" after they typed 8).
- Allow paste.
- Save progress.

### Empty states
- Explain what's missing.
- Show the path forward.
- Use illustrations thoughtfully.

### Loading states
- Skeletons > spinners (perceived performance).
- Show progress if known.
- Optimistic UI for instant feedback.

### Error states
- Explain what went wrong (user language).
- Show how to fix it.
- Allow retry.
- Don't blame the user.

### Microinteractions
Small moments of feedback:
- Button press.
- Toggle on/off.
- Save success toast.
- Subtle hover state.

→ [UX/microinteractions.md](microinteractions.md)

### Mobile UX
- Thumb zone for primary actions.
- Bottom sheets for actions.
- Swipe gestures (with discoverable alternatives).
- Large tap targets.
- No hover-only interactions.

### Accessibility is UX
Accessible = better UX for everyone. → [Accessibility/](../Accessibility/)

### Performance is UX
Fast = better UX. Slow = users leave. → [Performance/](../Performance/)

### Copy is UX
Words matter. Clear, concise, human. → [ANTI-AI-DESIGN/copywriting.md](../ANTI-AI-DESIGN/copywriting.md)

## Common UX Anti-Patterns

- ❌ Mystery meat navigation.
- ❌ Hiding important actions behind three menus.
- ❌ Disabling buttons without explanation.
- ❌ Auto-advancing forms.
- ❌ Forcing signup before seeing value.
- ❌ Long multi-step forms without progress.
- ❌ No empty state.
- ❌ Modal-on-modal.
- ❌ Auto-playing anything.
- ❌ Captchas everywhere.
- ❌ Confirming destructive actions with same-color buttons.

## Tools

- Figma: design.
- Maze / Useberry: prototype testing.
- Hotjar / FullStory / PostHog: session replay + heatmaps.
- UserTesting.com: moderated/unmoderated testing.
- Calendly + Zoom: user interviews.
- Tally / Typeform: surveys.

## References

- Nielsen Norman Group: https://www.nngroup.com/
- Smashing Magazine UX: https://www.smashingmagazine.com/category/ux
- UX Collective: https://uxdesign.cc/
- Laws of UX: https://lawsofux.com/
- UX Stack Exchange: https://ux.stackexchange.com/

## Further Reading

- *Don't Make Me Think* — Steve Krug
- *The Design of Everyday Things* — Don Norman
- *About Face* — Alan Cooper
- *Seductive Interaction Design* — Stephen Anderson
- *100 Things Every Designer Needs to Know About People* — Susan Weinschenk

## Exercises

1. Take a flow you use daily. Map every step.
2. Conduct a 5-user usability test on your project.
3. Redesign a form's UX (reduce friction by 30%).

## Projects

- Design an onboarding flow for a SaaS app (map → wireframe → prototype → test).
- Redesign an e-commerce checkout for fewer abandoned carts.

---

**Previous:** [UI/](../UI/) · **Next:** [Typography/](../Typography/) · **Related:** [ANTI-AI-DESIGN/](../ANTI-AI-DESIGN/)
