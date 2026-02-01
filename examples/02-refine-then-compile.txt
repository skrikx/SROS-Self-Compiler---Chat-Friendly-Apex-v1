# File: examples/02-refine-then-compile.txt

# SROS Self-Compiler (OSS) - Example 02: Refine then compile
# Goal: show intake form flow for vague requests.

USER
refine: website

ASSISTANT (expected)
<compiler_input_form xmlns="https://sros.cloud/schema/intake/v1">
  <how_to_use>
    Fast mode: start your message with "compile:" and write your goal.
    Refine mode: fill <compiler_input> and send it back.
  </how_to_use>
  <compiler_input>
    <goal><![CDATA[One paragraph. What do you want built or produced?]]></goal>
    <deliverables>
      <item><![CDATA[Pick one or more: website | app | docs | sr8_prompt | srx_ace_agent | promptunit_package | other]]></item>
    </deliverables>
    <constraints>
      <item><![CDATA[Hard constraints: local-only, no web, stack, pages, tone, size, deadlines, etc.]]></item>
    </constraints>
    <style_preferences>
      <item><![CDATA[Optional: brand colors, typography, motion, voice.]]></item>
    </style_preferences>
    <runtime>
      <capabilities>
        <tools>false</tools>
        <web>false</web>
        <vision>false</vision>
        <audio>false</audio>
        <video>false</video>
        <documents>false</documents>
      </capabilities>
    </runtime>
  </compiler_input>
</compiler_input_form>

USER (filled form)
<compiler_input xmlns="https://sros.cloud/schema/intake/v1">
  <goal><![CDATA[
Build a 10 page enterprise AI agency website for PlatXP (USA). Cobalt blue aesthetic, high polish.
  ]]></goal>

  <deliverables>
    <item>promptunit_package</item>
    <item>sr8_prompt</item>
  </deliverables>

  <constraints>
    <item>Stack must be SvelteKit + Tailwind + Motion One.</item>
    <item>Include sitemap, design tokens, copy brief.</item>
    <item>No backend build.</item>
  </constraints>

  <style_preferences>
    <item>Cobalt blue primary, slate-dark surface, electric-cyan accent.</item>
    <item>Authoritative, forward-leaning voice.</item>
  </style_preferences>

  <runtime>
    <capabilities>
      <tools>false</tools>
      <web>false</web>
      <vision>false</vision>
      <audio>false</audio>
      <video>false</video>
      <documents>false</documents>
    </capabilities>
  </runtime>
</compiler_input>

ASSISTANT (expected)
<promptunit_package xmlns="https://srx.sros/schema/package/v2">
  <package_meta>
    <package_id status="optional" kind="placeholder"/>
    <release_id status="optional" kind="placeholder"/>
    <timestamp status="optional" kind="placeholder"/>
    <compiler_version>OSS-Apex-1.0.0</compiler_version>
    <tenant_id>SROS</tenant_id>
    <operator_id>Skrikx Kyōten</operator_id>
  </package_meta>

  <governance_receipt>
    <classification>GENERAL_BUILD</classification>
    <decision>ALLOW</decision>
  </governance_receipt>

  <sr8_prompts>
    <active>
      <![CDATA[
<sr8_prompt id="SR8P.OSS.Active.v1" version="1.0.0" xmlns="https://sr8.sros/schema/prompt/v1">
  <role>SR8 Build Prompt</role>
  <objective>Compile the website blueprint into a complete manifest: sitemap, design specs, copy brief, acceptance tests.</objective>
</sr8_prompt>
      ]]>
    </active>
  </sr8_prompts>

  <compiler_run_report>
    <selected_lenses>LENS.SOVEREIGN.V1, LENS.DETERMINISM.V1</selected_lenses>
    <governance_decision>ALLOW</governance_decision>
    <active_sr8_prompt_id>SR8P.OSS.Active.v1</active_sr8_prompt_id>
  </compiler_run_report>
</promptunit_package>
