# System-driven Visual Content Testing

An automated n8n workflow that tests visual design systems by generating AI images and posting them to Pinterest. This workflow is designed for individual creators, solopreneurs, and smaller agencies who want to develop brand-consistent visuals and test audience engagement without the high costs of traditional design and A/B testing.

## What This Workflow Does

This workflow automates the entire visual content testing process, from idea generation to performance tracking. It combines AI image generation with human oversight to ensure quality while maintaining daily posting consistency.

### Main Features:
- **Daily automated posting** (9 AM trigger)
- **AI image generation** using Pollinations.ai with custom prompts
- **Human approval workflow** for quality control
- **Pinterest API integration** for automatic pin creation
- **Google Sheets integration** for content management
- **Analytics collection** for performance tracking

## How It Works

### Workflow 1: Pinterest Board Creation (Run Once)
1. **Fetch Visual System Data**: Retrieves data on active visual systems from Google Sheets
2. **Create System-Specific Pinterest Boards**: Loops through each system and creates corresponding Pinterest boards via API
3. **Store Board IDs**: Saves Pinterest board IDs back to Google Sheets for future use

### Workflow 2: Visual System Testing with Pinterest
1. **Daily Trigger**: Runs automatically every day at 9:00 AM
2. **Random Image Selection**: Retrieves unpublished content from the content queue sheet and randomly selects one item
3. **AI Image Generation**: Creates images using Pollinations.ai based on detailed prompts
4. **Google Drive Upload**: Saves generated images to Google Drive for backup and review
5. **Human Approval**: Sends approval email with image, prompt, and pin details. Workflow pauses until approval/decline
6. **Conditional Processing**:
   - **If Approved**: Posts pin to Pinterest and updates content queue sheet
   - **If Declined**: Sends review reminder email with content feedback

### Workflow 2 Extension: Analytics Collection
1. **Wait a Week**: Pauses for 7 days to gather engagement data
2. **Pin Analytics**: Retrieves performance metrics (impressions, clicks, saves) from Pinterest API
3. **Update Analytics**: Saves performance data to Google Sheets for analysis

## Prerequisites

- **Pinterest Business account** with API access (free, requires API token request)
- **Google Sheets** with populated:
  - `content_queue` sheet containing unpublished image prompts and pin details
  - `visual_systems` sheet with system parameters
- **Gmail account** for approval notifications
- **n8n instance** with the following integrations:
  - Google Sheets OAuth2
  - Google Drive OAuth2
  - Gmail OAuth2
  - Pinterest API access

## Setup Requirements

### Pinterest API
- Initial setup uses Sandbox endpoints (`https://api-sandbox.pinterest.com/v5`)
- Change to production endpoints (`https://api.pinterest.com/v5`) for live posting
- Trial access includes full Sandbox and limited Production access (read only)
- Standard access (for live pin creation and analytics) requires demo video submission to Pinterest

### Google Sheets Structure
The workflow expects two sheets with specific columns:

**content_queue sheet**:
- `content_id`, `system_id`, `system_name`, `success_dimensions`
- `image_prompt`, `pin_title`, `pin_description`, `alt_text`
- `posted`, `posted_at`, `platform`, `board_id`, `pin_id`
- Analytics fields: `impressions`, `outbound_clicks`, `pin_clicks`, `saves`, `save_rate`

**visual_systems sheet**:
- `system_id`, `system_name`, `brand_name`, `content_theme`
- `target_audience`, `success_dimensions`, `design_intent`
- Visual rules: `colour_rules`, `composition_rules`, `typography_style`
- `visual_style`, `texture_rules`, `prompt_instruction`, `prompt_constraints`
- `active`, `board_id`

## Image Generation Details

- **Service**: Pollinations.ai
- **Model**: Flux
- **Dimensions**: 1000x1500 pixels (Pinterest optimal)
- **Prompt Engineering**: Uses detailed visual system parameters from Google Sheets

## Usage Instructions

1. **First Time Setup**: Run Workflow 1 manually to create Pinterest boards and store board IDs
2. **Daily Operation**: Workflow 2 runs automatically at 9 AM
3. **Approval Process**: Check your email daily to approve/decline generated content
4. **Performance Tracking**: Review Google Sheets weekly for analytics data

## Benefits

- **Cost Effective**: Eliminates need for expensive design tools and A/B testing
- **Brand Consistency**: Maintains visual coherence across all content
- **Time Saving**: Automates daily posting while maintaining quality control
- **Data-Driven**: Collects real performance data for continuous improvement (with Pinterest Standard API Access only)
- **Scalable**: Easy to add new visual systems and content variations

## Limitations

- **Pinterest API Constraints**: Live pin creation and analytics collection require Standard API access
- **Sandbox vs Production**: Initial setup uses sandbox environment
- **Manual Approval Required**: Human oversight needed for quality control
- **Rate Limits**: Subject to Pinterest API rate limits

## Workflow Variants

### Original Workflow: System-driven Visual Content Testing.json
The original n8n workflow that uses Pinterest's Sandbox API for testing. This version is ideal for initial testing and development but has limitations for live pin creation.

### Updated Workflow: System-driven Visual Content Testing v2.json
An enhanced version of the original workflow that uses **LATE API** instead of Pinterest's direct API for posting pins. Key differences:

- **Live Pin Creation**: Uses LATE API (`https://getlate.dev/api/v1/posts`) for actual pin posting, not just sandbox testing
- **Simplified Board Setup**: Boards are created manually on Pinterest, then fetched via API
- **LATE Integration**: Requires LATE account connected to Pinterest (free for 20 posts/month)
- **Pinterest Account ID**: Required from LATE dashboard for authentication
- **Analytics Option**: LATE offers analytics add-on ($1/social set/month) as alternative to Pinterest Standard API

### Make Alternative: Create Pinterest pins from Google Sheets data using Pollination AI Make.blueprint.json
A Make.com blueprint version of the same automation workflow that uses Make's Pinterest module instead of n8n. This provides:
- **Make.com Interface**: Alternative to n8n for users who prefer Make's visual workflow builder
- **Pinterest Module**: Uses Make's native Pinterest integration instead of direct API calls
- **Same Core Functionality**: Google Sheets integration, Pollinations AI image generation, and Pinterest posting

## Spreadsheet Templates

Two spreadsheet templates are included for easy setup:

### Visual System Testing with Pinterest.xlsx
Template designed specifically for the n8n workflows with the required sheet structure:
- `content_queue` sheet for managing image prompts and pin details
- `visual_systems` sheet for visual system parameters and board IDs
- Pre-formatted columns matching the workflow requirements

### Visual Systems Testing - Make.xlsx
Template optimised for the Make.com blueprint with corresponding structure for Make modules.

## Demo Video

A demo video showing the n8n workflow in action with Pinterest API integration is available. This video demonstrates:
- Workflow setup and configuration
- AI image generation process
- Human approval workflow
- Pin creation to Pinterest

---

**Subscribe to [Savvy Sloth Substack](https://savvysloth.substack.com) for detailed setup instructions, including AI prompts to generate visual systems and image prompts for Google Sheets, and for more workflows and automations!**
