# Analytics

> Measure what matters. Respect user privacy.

---

## Purpose

Track user behavior, product metrics, and business KPIs without being creepy.

## Prerequisites

- [JavaScript/](../JavaScript/).

## Learning Outcome

You can pick the right analytics tool, instrument events, and respect user privacy.

## Dependencies

- None.

## Related Files

- [SEO/](../SEO/) · [Performance/](../Performance/) · [Monitoring/](../Monitoring/) · [Security/ai.md](../Security/ai.md) (privacy)

## AI Instructions

When adding analytics:
1. **Pick one** primary tool. Don't pile on 5 trackers.
2. **Define events** upfront (event name, properties).
3. **Respect Do Not Track** and consent banners.
4. **No PII** in event properties.
5. **Document the event schema**.
6. **Use server-side analytics** for sensitive data.

## Human Notes

### Tool categories
- **Web analytics** — traffic, page views (GA4, Plausible, Umami, Fathom).
- **Product analytics** — funnels, retention (PostHog, Mixpanel, Heap, Amplitude).
- **Session replay** — watch real sessions (FullStory, LogRocket, PostHog).
- **Error tracking** — exceptions (Sentry, Highlight).
- **A/B testing** — experiments (PostHog, GrowthBook, Optimizely).

### Picks by need
| Need | Pick |
|---|---|
| Privacy-friendly simple | Plausible, Fathom, Umami |
| Comprehensive product | PostHog (open-source, all-in-one) |
| Industry default | GA4 (privacy-invasive but standard) |
| Enterprise product | Mixpanel, Amplitude |
| Session replay | PostHog (free), FullStory, LogRocket |
| A/B testing | PostHog, GrowthBook (open-source) |
| Error tracking | Sentry, Highlight |

### PostHog setup (recommended)
```html
<script>
  !function(t,e){var o,n,p,r;e.__SV||(window.posthog=e,e._i=[],e.init=function(i,s,a){function g(t,e){var o=e.split(".");2==o.length&&(t=t[o[0]],e=o[1])}t._i.push([i,s,a])},e.__SV=1)}(document,window.posthog||[]);
  posthog.init('YOUR_KEY', { api_host: 'https://app.posthog.com' });
</script>
```

```js
posthog.capture('button_clicked', { button_id: 'signup' });
posthog.identify('user-123', { email: 'a@b.com' });
```

### Event design
- Names: `noun_verb_past_tense` (e.g., `user_signed_up`).
- Properties: snake_case, primitive values.
- Don't track PII in properties.
- Version your schema.

### Privacy
- Show cookie banner (if required in your jurisdiction).
- Respect Do Not Track.
- Allow opt-out.
- Don't track PII without consent.
- Consider server-side analytics (no client JS).

### Server-side analytics
- Track on the server.
- No client JS = no third-party requests.
- Better privacy, better ad blockers don't break.
- Plausible, Fathom, PostHog all support this.

### Funnels
Map your funnel: visit → signup → activation → retention → revenue.
Track conversion at each step.

### Retention
- Day 1, Day 7, Day 30 retention.
- Cohort analysis.
- Compare to industry benchmarks.

### A/B testing
- Hypothesis first.
- One variable.
- Statistical significance (not "looks better").
- Run long enough.
- Don't peek.

## Common Mistakes

- ❌ Multiple trackers (GA + Mixpanel + Hotjar + ...).
- ❌ Tracking everything (signal lost in noise).
- ❌ No event schema (everyone uses different names).
- ❌ PII in events.
- ❌ No consent banner (where required).
- ❌ Not respecting DNT.
- ❌ Vanity metrics (pageviews) over actionable metrics (activation).

## Tools

- PostHog: https://posthog.com/
- Plausible: https://plausible.io/
- Umami: https://umami.is/
- Fathom: https://usefathom.com/
- GA4: https://analytics.google.com/
- Mixpanel: https://mixpanel.com/
- Amplitude: https://amplitude.com/
- Heap: https://heap.io/
- FullStory: https://www.fullstory.com/
- LogRocket: https://logrocket.com/
- GrowthBook: https://www.growthbook.io/
- Highlight.io: https://www.highlight.io/

## References

- PostHog docs: https://posthog.com/docs
- Plausible docs: https://plausible.io/docs
- web.dev metrics: https://web.dev/articles/metrics

## Exercises

1. Set up PostHog (free tier). Track signup funnel.
2. Define your event schema (doc).
3. Build a retention dashboard.

## Projects

- Build an analytics pipeline: events → Postgres → dashboard.

---

**Previous:** [SEO/](../SEO/) · **Next:** [Authentication/](../Authentication/) · **Related:** [Monitoring/](../Monitoring/)
