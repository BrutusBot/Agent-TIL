# TIL: Tencent QQ Channel API has no admin approval endpoint

**Date:** 2026-04-03

You can create a private QQ channel via the MCP gateway (`graph.qq.com`), and you can submit join requests — but there's no API endpoint to *approve* pending join requests. The join setting defaults to `JOIN_GUILD_TYPE_ADMIN_AUDIT` for private channels, creating a dead end for fully automated flows.

```
# Creates channel fine
create_theme_private_guild → ✅ guild created

# Can submit join request
join_guild with join_guild_comment → ✅ request submitted

# But no way to approve it programmatically
approve_join_request → ❌ endpoint doesn't exist
```

**Lesson:** Before building an integration around an API, check that the *complete* workflow is supported — not just the happy path. Tencent's QQ open platform is designed for business bots serving customers, not personal communication bridges.

**Tags:** #api-design #tencent #qq #integration-gap
