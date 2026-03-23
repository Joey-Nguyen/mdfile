# Layout Config JSON Spec — Web + Jetpack Compose Mapping


## 1. Page Config & Theme

Mỗi page JSON bọc trong object `page` chứa `style`, `theme`, `scrollBehavior`, và `sections[]`.

### Style Cascade — Nguyên tắc ưu tiên style

Toàn bộ cấu trúc JSON tuân theo nguyên tắc style cascade 3 cấp:

```
Level 1: page.theme       — Global defaults (colors, typography, spacing, focus)
Level 2: section.style    — Override cho section cụ thể
Level 3: item.style       — Override cho item cụ thể
```

| Level | Scope | Khi nào dùng |
|---|---|---|
| `page.theme` | Toàn page | Default colors, fonts, spacing, focus cho mọi section |
| `section.style` | 1 section | Section background, padding, title style, item spacing khác default |
| `itemConfig.style` | Items trong section | Card style, focus style, text style khác default |
| `item.style` (inline) | 1 item cụ thể | Highlight 1 item đặc biệt (featured, sponsored) |


## 2. Page JSON

```json
{
  "schemaVersion": "1.0",
  "page": {
    "skinId": "basic",
    "themeSource": {
      "skinOverrides": {},
      "customOverrides": {}
    },
    "style": {
      "background": "#0a0a1a",
      "backgroundImage": null,
      "backgroundScaleType": "center_crop",
      "paddingTop": 0,
      "paddingBottom": 0,
      "paddingStart": 0,
      "paddingEnd": 0
    },
    "decorations": [],
    "theme": {
      "colors": {
        "primary": "#3b82f6",
        "primaryVariant": "#2563eb",
        "secondary": "#f97316",
        "surface": "#1a1a2e",
        "background": "#0a0a1a",
        "onPrimary": "#ffffff",
        "onSurface": "#e0e0e0",
        "onBackground": "#ffffff",
        "error": "#ef4444",
        "divider": "#333333"
      },
      "typography": {
        "headingSize": 24,
        "titleSize": 18,
        "bodySize": 14,
        "captionSize": 12,
        "defaultFontFamily": "sans-serif",
        "defaultTextColor": "#ffffff"
      },
      "spacing": {
        "sectionGap": 24,
        "railPaddingHorizontal": 24,
        "itemSpacing": 8
      },
      "focusStyle": {
        "borderWidth": 2,
        "borderColor": "#3b82f6",
        "scaleX": 1.05,
        "scaleY": 1.05,
        "elevation": 8
      }
    },
    "scrollBehavior": {
      "orientation": "vertical",
      "overscrollEffect": "glow",
      "rememberPosition": true,
      "smoothScroll": true
    }
  },
  "sections": [
    {
      "id": "sec-gnb",
      "name": "GNB Menu",
      "moduleType": "gnb_menu",
      "layout": {
        "type": "row",
        "width": "match_parent",
        "height": 48,
        "position": "fixed",
        "overlay": true,
        "zIndex": 100
      },
      "style": {
        "background": "rgba(0,0,0,0.8)",
        "paddingStart": 24,
        "paddingEnd": 24
      },
      "columns": [
        {
          "id": "nav",
          "gravity": "start",
          "gap": 24,
          "style": {
            "textSize": 14,
            "fontFamily": "sans-serif-medium",
            "textColor": "#888888",
            "activeTextColor": "#ffffff",
            "activeBorderBottom": 2,
            "activeBorderColor": "#3b82f6",
            "hoverTextColor": "#cccccc"
          },
          "items": [
            { "label": "HOME", "slug": "home", "isVisible": true },
            { "label": "VOD", "slug": "vod", "isVisible": true },
            { "label": "LIVE TV", "slug": "live-tv", "isVisible": true },
            { "label": "KIDS", "slug": "kids", "isVisible": true },
            { "label": "OTT", "slug": "ott", "isVisible": true },
            { "label": "APPS", "slug": "apps", "isVisible": true }
          ]
        },
        {
          "id": "actions",
          "gravity": "end",
          "gap": 16,
          "style": {
            "iconSize": 24,
            "iconColor": "#ffffff",
            "hoverIconColor": "#3b82f6",
            "badgeBackground": "#ef4444",
            "badgeTextColor": "#ffffff",
            "badgeSize": 8
          },
          "items": [
            { "icon": "search", "action": "open_search", "isVisible": true },
            { "icon": "notifications", "action": "open_notifications", "isVisible": true, "badge": 3 },
            { "icon": "settings", "action": "open_settings", "isVisible": true },
            { "icon": "user", "action": "open_profile", "isVisible": true, "imageUrl": "https://cdn.example.com/avatars/default.png" }
          ]
        }
      ]
    },

    {
      "id": "sec-hero",
      "name": "Hero Banner",
      "moduleType": "banner",
      "layout": {
        "type": "carousel",
        "width": "match_parent",
        "height": 420,
        "autoScroll": true,
        "autoScrollInterval": 5000,
        "showIndicator": true,
        "indicatorPosition": "bottom_start",
        "infiniteLoop": true
      },
      "slides": [
        {
          "id": "slide-1",
          "background": {
            "videoUrl": "https://cdn.example.com/abigail-trailer.mp4",
            "stillImageUrl": "https://cdn.example.com/abigail-still.jpg"
          },
          "deepLink": "app://content/abigail",
          "sortOrder": 0,
          "elements": [
            {
              "id": "el-logo",
              "type": "image",
              "src": "https://cdn.example.com/abigail-logo.png",
              "position": { "x": 48, "y": 180, "anchor": "bottom_start" },
              "size": { "width": 200, "height": 60 }
            },
            {
              "id": "el-title",
              "type": "text",
              "content": "ABIGAIL",
              "position": { "x": 48, "y": 220, "anchor": "bottom_start" },
              "font": { "family": "sans-serif-medium", "size": 32, "weight": "bold", "color": "#ffffff" }
            },
            {
              "id": "el-desc",
              "type": "text",
              "content": "A group of criminals kidnaps a teenage ballet dancer...",
              "position": { "x": 48, "y": 260, "anchor": "bottom_start" },
              "font": { "size": 14, "color": "#cccccc" },
              "maxWidth": 480,
              "maxLines": 2
            },
            {
              "id": "el-sub",
              "type": "text",
              "content": "2024 | Action, Horror",
              "position": { "x": 48, "y": 288, "anchor": "bottom_start" },
              "font": { "size": 12, "color": "#aaaaaa" }
            },
            {
              "id": "el-btn",
              "type": "button",
              "label": "MORE",
              "action": "open_detail",
              "deepLink": "app://content/abigail",
              "position": { "x": 48, "y": 320, "anchor": "bottom_start" },
              "style": {
                "background": "#3b82f6",
                "textColor": "#ffffff",
                "cornerRadius": 4,
                "paddingHorizontal": 24,
                "paddingVertical": 8,
                "font": { "size": 14, "weight": "bold" }
              }
            }
          ]
        },
        {
          "id": "slide-2",
          "background": {
            "videoUrl": "https://cdn.example.com/dune2-trailer.mp4",
            "stillImageUrl": "https://cdn.example.com/dune2-still.jpg"
          },
          "deepLink": "app://content/dune-part-two",
          "sortOrder": 1,
          "elements": [
            {
              "id": "el-logo",
              "type": "image",
              "src": "https://cdn.example.com/dune2-logo.png",
              "position": { "x": 48, "y": 200, "anchor": "bottom_start" },
              "size": { "width": 220, "height": 70 }
            },
            {
              "id": "el-title",
              "type": "text",
              "content": "DUNE PART TWO",
              "position": { "x": 48, "y": 260, "anchor": "bottom_start" },
              "font": { "size": 32, "weight": "bold", "color": "#ffffff" }
            },
            {
              "id": "el-btn",
              "type": "button",
              "label": "MORE",
              "action": "open_detail",
              "deepLink": "app://content/dune-part-two",
              "position": { "x": 48, "y": 320, "anchor": "bottom_start" },
              "style": {
                "background": "#3b82f6",
                "textColor": "#ffffff",
                "cornerRadius": 4,
                "paddingHorizontal": 24,
                "paddingVertical": 8,
                "font": { "size": 14, "weight": "bold" }
              }
            }
          ]
        }
      ]
    },

    {
      "id": "sec-fav-apps",
      "name": "Favorite Apps",
      "moduleType": "vod_content_list",
      "layout": {
        "type": "scroll_row",
        "orientation": "horizontal",
        "height": "wrap_content",
        "snap": "start"
      },
      "title": {
        "text": "Favorite Apps",
        "isVisible": true,
        "type": "text"
      },
      "layoutVariant": "thumbnails",
      "frameSize": "S",
      "style": {
        "marginTop": 16,
        "paddingStart": 24,
        "paddingEnd": 24,
        "titleStyle": {
          "textSize": 18,
          "textColor": "#ffffff",
          "fontWeight": "bold",
          "fontFamily": "sans-serif-medium",
          "marginBottom": 12
        }
      },
      "itemConfig": {
        "width": 80,
        "height": 80,
        "spacing": 12,
        "style": {
          "cornerRadius": 16,
          "background": "#1a1a2e",
          "elevation": 2,
          "titleStyle": {
            "textSize": 11,
            "textColor": "#cccccc",
            "fontWeight": "normal",
            "marginTop": 4
          },
          "focusStyle": {
            "borderWidth": 2,
            "borderColor": "#3b82f6",
            "scaleX": 1.05,
            "scaleY": 1.05,
            "elevation": 8
          }
        },
        "showImage": true,
        "showTitle": true,
        "showRanking": false,
        "showProgressBar": false,
        "showLogo": false
      },
      "dataSource": {
        "type": "local",
        "provider": "favorite_apps",
        "emptyState": {
          "message": "Add your favorite apps",
          "action": "open_app_store",
          "hidden": false
        }
      },
      "items": [
        {
          "id": "app-netflix",
          "imageUrl": "https://cdn.example.com/apps/netflix-icon.png",
          "title": "Netflix",
          "deepLink": "app://package/com.netflix.mediaclient",
          "metadata": { "packageName": "com.netflix.mediaclient" }
        },
        {
          "id": "app-youtube",
          "imageUrl": "https://cdn.example.com/apps/youtube-icon.png",
          "title": "YouTube",
          "deepLink": "app://package/com.google.android.youtube.tv",
          "metadata": { "packageName": "com.google.android.youtube.tv" }
        },
        {
          "id": "app-disney",
          "imageUrl": "https://cdn.example.com/apps/disney-icon.png",
          "title": "Disney+",
          "deepLink": "app://package/com.disney.disneyplus",
          "metadata": { "packageName": "com.disney.disneyplus" },
          "style": {
            "_comment": "Promoted app — wider card with accent border",
            "width": 120,
            "height": 80,
            "cornerRadius": 12,
            "borderWidth": 2,
            "borderColor": "#1d4ed8",
            "background": "#0c1a3d",
            "titleStyle": {
              "textColor": "#60a5fa",
              "fontWeight": "bold"
            }
          }
        },
        {
          "id": "app-add",
          "imageUrl": null,
          "title": "Add App",
          "deepLink": null,
          "metadata": { "action": "open_app_store" },
          "style": {
            "_comment": "Add button — dashed border, no background, icon-only",
            "background": "transparent",
            "borderWidth": 1,
            "borderColor": "#555555",
            "borderStyle": "dashed",
            "cornerRadius": 16,
            "icon": "add",
            "iconColor": "#888888",
            "titleStyle": {
              "textSize": 10,
              "textColor": "#888888"
            }
          }
        }
      ]
    },

    {
      "id": "sec-netflix",
      "name": "Netflix",
      "moduleType": "ott_content_list",
      "layoutVariant": "thumbnails_with_logo_top",
      "frameSize": "M",
      "layout": {
        "type": "scroll_row",
        "orientation": "horizontal",
        "height": "wrap_content",
        "snap": "start"
      },
      "title": {
        "text": "Netflix",
        "isVisible": true,
        "type": "text",
        "icon": { "text": "N", "background": "#e50914", "cornerRadius": 4 }
      },
      "style": {
        "marginTop": 24,
        "paddingStart": 24,
        "paddingEnd": 24,
        "background": "#141414",
        "titleStyle": {
          "textSize": 18,
          "textColor": "#ffffff",
          "fontWeight": "bold",
          "fontFamily": "sans-serif-medium",
          "marginBottom": 12
        }
      },
      "itemConfig": {
        "width": 180,
        "height": 120,
        "spacing": 8,
        "style": {
          "cornerRadius": 4,
          "background": "#262626",
          "elevation": 2,
          "borderWidth": 0,
          "focusStyle": {
            "borderWidth": 2,
            "borderColor": "#e50914",
            "scaleX": 1.05,
            "scaleY": 1.05,
            "elevation": 8
          }
        },
        "showImage": true,
        "showTitle": false,
        "showLogo": true,
        "showRanking": false,
        "showProgressBar": false
      },
      "dataSource": {
        "type": "remote",
        "provider": "netflix",
        "endpoint": "content://com.netflix.mediaclient/trending",
        "params": { "limit": 20 },
        "cache": { "ttl": 1800, "strategy": "cache_first" },
        "fallback": {
          "type": "server",
          "endpoint": "/api/v1/content/netflix-cache"
        },
        "visibility": { "minItems": 1 }
      },
      "items": [
        {
          "id": "nf-1",
          "imageUrl": "https://cdn.example.com/netflix/squid-game-2.jpg",
          "title": "Squid Game Season 2",
          "deepLink": "app://content/squid-game-2",
          "logoUrl": "https://cdn.example.com/netflix/netflix-logo-sm.png",
          "metadata": { "year": "2024", "genre": "Thriller" }
        },
        {
          "id": "nf-2",
          "imageUrl": "https://cdn.example.com/netflix/wednesday-s2.jpg",
          "title": "Wednesday Season 2",
          "deepLink": "app://content/wednesday-s2",
          "logoUrl": "https://cdn.example.com/netflix/netflix-logo-sm.png",
          "metadata": { "year": "2025", "genre": "Comedy, Horror" },
          "style": {
            "_comment": "Featured — double width spotlight card",
            "width": 368,
            "height": 160,
            "cornerRadius": 8,
            "borderWidth": 2,
            "borderColor": "#e50914",
            "background": "#1a0000",
            "overlay": {
              "badge": "NEW",
              "badgeBackground": "#e50914",
              "badgePosition": "top_end",
              "gradient": "linear-gradient(transparent 50%, rgba(0,0,0,0.8) 100%)"
            },
            "titleStyle": {
              "textSize": 16,
              "textColor": "#ffffff",
              "fontWeight": "bold",
              "position": "bottom_start",
              "paddingStart": 12,
              "paddingBottom": 8
            },
            "focusStyle": {
              "borderWidth": 3,
              "borderColor": "#ff1a1a",
              "scaleX": 1.03,
              "scaleY": 1.03,
              "elevation": 12
            }
          }
        },
        {
          "id": "nf-3",
          "imageUrl": "https://cdn.example.com/netflix/stranger-things.jpg",
          "title": "Stranger Things",
          "deepLink": "app://content/stranger-things",
          "logoUrl": "https://cdn.example.com/netflix/netflix-logo-sm.png",
          "metadata": { "year": "2025", "genre": "Sci-Fi" }
        },
        {
          "id": "nf-4",
          "imageUrl": "https://cdn.example.com/netflix/the-night-agent.jpg",
          "title": "The Night Agent",
          "deepLink": "app://content/night-agent",
          "logoUrl": "https://cdn.example.com/netflix/netflix-logo-sm.png",
          "metadata": { "year": "2024", "genre": "Action" },
          "style": {
            "_comment": "Continued watching — show progress bar + resume text",
            "showProgressBar": true,
            "progress": 0.65,
            "progressBarStyle": {
              "height": 4,
              "fillColor": "#e50914",
              "background": "#333333"
            },
            "subtitleText": "S2 E4 · 38 min left",
            "subtitleStyle": {
              "textSize": 10,
              "textColor": "#999999",
              "marginTop": 4
            }
          }
        }
      ]
    },

    {
      "id": "sec-apple-tv",
      "name": "Apple TV",
      "moduleType": "ott_content_list",
      "layoutVariant": "thumbnails_with_logo_top",
      "frameSize": "M",
      "layout": {
        "type": "scroll_row",
        "orientation": "horizontal",
        "height": "wrap_content",
        "snap": "start"
      },
      "title": {
        "text": "Apple TV",
        "isVisible": true,
        "type": "text",
        "icon": { "imageUrl": "https://cdn.example.com/ott/appletv-icon.png", "width": 24, "height": 24 }
      },
      "style": {
        "marginTop": 24,
        "paddingStart": 24,
        "paddingEnd": 24,
        "titleStyle": {
          "textSize": 18,
          "textColor": "#ffffff",
          "fontWeight": "bold",
          "fontFamily": "sans-serif-medium",
          "marginBottom": 12
        }
      },
      "itemConfig": {
        "width": 180,
        "height": 120,
        "spacing": 8,
        "style": {
          "cornerRadius": 8,
          "background": "#1a1a2e",
          "elevation": 2,
          "borderWidth": 0,
          "focusStyle": {
            "borderWidth": 2,
            "borderColor": "#3b82f6",
            "scaleX": 1.05,
            "scaleY": 1.05,
            "elevation": 8
          }
        },
        "showImage": true,
        "showTitle": false,
        "showLogo": true,
        "showRanking": false,
        "showProgressBar": false
      },
      "dataSource": {
        "type": "remote",
        "provider": "apple_tv",
        "endpoint": "content://com.apple.tv/catalog",
        "fallback": {
          "type": "server",
          "endpoint": "/api/v1/content/appletv-cache"
        },
        "visibility": { "minItems": 1 }
      },
      "items": []
    }
  ]
}
```

### Per-item Style Override — Resolution Examples

Khi render 1 item, style được resolve theo cascade: `item.style` → `itemConfig.style` → `page.theme`.

## Naming Convention Summary

| Concept | JSON field name | Based on |
|---------|----------------|----------|
| Size | `match_parent`, `wrap_content` | Android `LayoutParams` |
| Margin/Padding | `marginStart`, `paddingEnd` | Android RTL-aware naming |
| Alignment | `gravity`, `verticalGravity` | Android `Gravity` |
| Flex distribution | `weight` | Android `layout_weight` |
| Background | `background` | Android + CSS both use this |
| Corner | `cornerRadius` | Android `GradientDrawable` |
| Shadow | `elevation` | Android `View.elevation` |
| Transparency | `alpha` | Android `View.alpha` |
| Text size | `textSize` | Android `TextView.textSize` (sp) |
| Focus highlight | `focusStyle` | Android TV D-pad navigation |
| Skin/Theme | `skinId`, `decorations` | Predefined theme overrides |
| Theme layers | `themeSource.skinOverrides`, `customOverrides` | 3-layer merge system |
| Theme colors | `primary`, `surface`, `onPrimary` | Android Material Design naming |
| Overlay decoration | `overlay_image`, `position` | Seasonal skin assets |
| Module type | `moduleType` | Editor module category (banner, vod_content_list, ott_content_list, gnb_menu, ad_widget, banner_list) |
| Style cascade | `page.theme` → `section.style` → `itemConfig.style` → `item.style` | 3-level style inheritance: global → section → item |
| Menu columns | `columns[]` | GNB menu — column groups: nav links + action buttons |
| Column style | `columns[].style` | Per-column style (nav text style, action icon style) |
| Action buttons | `columns[].items[]` with `icon` + `action` | Fixed utility: search, notifications, settings, user |
| Section style | `section.style` | Override theme for specific section (background, padding, titleStyle) |
| Item config | `itemConfig` | Content rail item display: size, spacing, show flags |
| Item style | `itemConfig.style` | Default card style for items (cornerRadius, focusStyle, titleStyle) |
| Inline item style | `item.style` | Per-item override (featured/sponsored highlight) |
| Title style | `style.titleStyle` | Section heading style (textSize, textColor, fontWeight) |
| Focus style | `style.focusStyle` or `page.theme.focusStyle` | D-pad focus highlight (border, scale, elevation) |
| Ranking style | `style.rankingStyle` | Overlay ranking number style |
| Progress bar | `style.progressBarStyle` | Watch progress bar style |
| Banner slides | `slides[]` | Hero banner multi-slide carousel |
| Slide elements | `elements[]` | Free-form text/image/button/link on banner with position + font |
| Element position | `position: { x, y, anchor }` | Absolute positioning within slide (anchor: top_start, bottom_start, center...) |
| Element font | `font: { family, size, weight, color }` | Per-element typography |
| Layout variant | `layoutVariant` | Section-level: thumbnails, posters_with_ranking, etc. |
| Frame size | `frameSize` | Section-level: S, M, L |
| Section title | `title: { text, isVisible, icon }` | Section header with optional icon |
| Ad config | `adConfig` | Inline ad (landing, tracking) |
