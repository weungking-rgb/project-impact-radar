# Project News Monitor

A personalized news monitoring Skill that connects the latest industry information with your ongoing projects, and pushes only the updates that actually matter.

## What This Skill Does

1. **Custom Domain Monitoring**  
   You define the technical domains you care about (e.g. Rockchip RV1106, Quectel modules, smart glasses assistive technology, government subsidies). The Skill guides the agent to fetch the latest relevant news every day.

2. **Project Impact Matching**  
   After you upload your current project descriptions, the Skill analyzes news against your projects and only surfaces items that may impact them — technical changes, competitor moves, supply chain issues, regulations, market signals, etc.

3. **Structured Impact Digest**  
   Delivers a clear daily summary grouped by High Impact and Medium/Watch, with suggested next actions.

## Who Is This For

- Hardware / IoT / smart device product managers and engineers
- Teams tracking chips, modules, certifications, and subsidy policies
- Anyone who wants industry news tightly linked to their product roadmap
- People working on assistive technology, smart glasses, or edge AI products

## How to Use

### Step 1: Initial Setup

Tell the agent something like this:

```
Please set up project news monitoring for me.

Monitoring domains:
1. Rockchip RV1106 / RK1106 related chips and SDKs
2. Quectel 4G modules (especially EG800Q series)
3. China smart hardware and IoT subsidy policies
4. Smart glasses / assistive technology

My current project:
- Project name: OpenClaw Smart Glasses
- Description: An AI agent-based wearable device that helps users with arm loss, visual impairment, or speech impairment complete daily and work tasks...
- High-impact keywords: chip power consumption, module stability, privacy compliance, assistive technology standards, government subsidies, competitor launches
```

### Step 2: Daily Usage

Simply say:

```
Run today’s project impact digest
```

or

```
运行今天的项目影响新闻摘要
```

### Step 3: Update Domains or Projects

Add a new domain:

```
Add a new monitoring domain: Type-C fast charging standards and reliability
```

Update a project:

```
Update project description: North American 4G dual-camera dashcam, focus on AOV low power and FCC certification
```

## File Structure

| File | Description |
|------|-------------|
| `SKILL.md` | Core instruction file for the Skill |
| `example-prompts.md` | Complete example prompts for setup and daily use |

## Notes

- True unattended daily push requires the Automations feature (scheduled tasks).
- Matching quality depends heavily on how specific and keyword-rich your project descriptions are.
- Both Chinese and English are fully supported.

## License

MIT
```

---

直接全选删除当前内容，然后粘贴上面这一整段即可。
