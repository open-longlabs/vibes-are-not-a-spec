# Database LARP

You say: protect my users' data, is my database safe

Paste this together with the [rules](00-rules.md) into your coding agent.

```
Database LARP.
Assume any row can be read or changed by the wrong person, script or AI tool until a
test proves otherwise.
Identify the database first: these checks target Supabase and PostgreSQL; on another
stack map each check to its equivalent or mark it NOT APPLICABLE with a reason.
Inventory every table, view and function in schemas the client API exposes, every
storage bucket, every use of a secret key (service_role, sb_secret_, database password
or connection string) and every AI tool or MCP server connected to the database with the
credentials it uses.
Per table: RLS on or off, every policy with command, role, USING and WITH CHECK and the
grants client roles hold.
Then probe anonymously with the publishable key and no user token and as user A and user
B with that key plus each user's own valid token:

(1) tables in an exposed schema with RLS off and client grants;
(2) policies broader than the access matrix (applicable permissive policies combine with
    OR and restrictive ones with AND, so judge each policy's role, command, USING and
    WITH CHECK together with grants);
(3) users updating their own row can also set role, plan, credits or verified, or move
    user_id to someone else;
(4) views without security_invoker and client-callable SECURITY DEFINER functions
    returning rows the caller may not see;
(5) a secret key in frontend code, the built bundle, source maps, the repo, git history,
    CI logs or an MCP config;
(6) functions building SQL from text with EXECUTE;
(7) backend routes using the secret key without their own object check;
(8) an AI tool that can read private data and also reads text users wrote (tickets,
    comments, profiles, documents), only if one exists;
(9) public buckets holding private files;
(10) no backups or point-in-time recovery, schema changed by hand on production;
(11) integration tokens or personal data readable by anyone with table access.

For each finding: severity, the query or request and result that prove it, the fix (RLS
plus per-operation policies from the access matrix using (select auth.uid()); revoke
table-level UPDATE from every applicable client role, including inherited grants, then
grant UPDATE only on approved columns; change sensitive columns through a server
function that checks the caller's permission; security_invoker on views, execute revoked
or an auth check plus fixed search_path on definer functions; leaked secret keys listed
for me to rotate; AI tools stripped of secrets and unneeded data first, read-only,
scoped, no free SQL where a narrow function works, every sensitive read and every write
shown to me before it runs, nothing they write lands where users can see it unreviewed)
and the guardrail: a test as a real user with its allowed twin.
A model refusing a planted instruction once proves nothing: prove the tool can't reach
the data.
```

**What it covers:** tables anyone can read with your public key, users giving themselves admin or credits, hidden ways around your row rules, leaked admin keys and AI tools with database access being steered by text your users wrote.
**Real cases:** [CVE-2025-48757](https://mattpalmer.io/posts/2025/05/CVE-2025-48757/): Lovable apps with missing RLS. [General Analysis](https://generalanalysis.com/blog/supabase-mcp-blog): in a July 2025 controlled demo with dummy data, an instruction hidden in a support ticket made a developer's MCP assistant with service_role access copy a private token table into a customer-visible reply.
**Sources:** [Supabase RLS](https://supabase.com/docs/guides/database/postgres/row-level-security) · [Supabase securing your API](https://supabase.com/docs/guides/api/securing-your-api) · [Supabase column level security](https://supabase.com/docs/guides/database/postgres/column-level-security) · [Supabase MCP](https://supabase.com/docs/guides/ai-tools/mcp) · [PostgreSQL CREATE VIEW](https://www.postgresql.org/docs/current/sql-createview.html) · [OWASP LLM01](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
