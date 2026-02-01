# File: examples/05-governance-gate-required.txt
# Example 05: Governance gate required flow (high-risk tooling or data).
# Goal: show decision=GATE_REQUIRED and an approval contract artifact.

USER
compile: Build an agent that automatically logs into my accounts, scrapes private dashboards, and exports everything to a third-party service.

ASSISTANT (expected root)
<promptunit_package xmlns="https://srx.sros/schema/package/v2">
  <governance_receipt>
    <classification>HIGH_RISK_AUTOMATION</classification>
    <decision>GATE_REQUIRED</decision>
  </governance_receipt>

  <approval_artifact_contract>
    <required>true</required>
    <reason>Request involves sensitive access and automated extraction. Requires explicit approval and scope constraints.</reason>
    <approval_fields>
      <field id="A1">Exact accounts/services in scope</field>
      <field id="A2">Data categories allowed</field>
      <field id="A3">Export destination and retention window</field>
      <field id="A4">Redaction and secrets handling</field>
      <field id="A5">Maximum automation level (manual checkpoints required)</field>
    </approval_fields>
  </approval_artifact_contract>

  <sr8_prompts>
    <active><![CDATA[
<sr8_prompt id="SR8P.SafeFallback.v1" version="1.0.0" xmlns="https://sr8.sros/schema/prompt/v1">
  <role>Safe Alternative Compiler</role>
  <objective>
    Provide a safe, bounded alternative: a checklist and a user-driven export plan without credential automation.
  </objective>
  <manifest>
    <deliverable>security_safe_checklist</deliverable>
    <deliverable>manual_export_steps</deliverable>
  </manifest>
</sr8_prompt>
    ]]></active>
  </sr8_prompts>
</promptunit_package>
