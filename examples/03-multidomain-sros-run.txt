# File: examples/03-multidomain-sros-run.txt
# Example 03: Multi-domain compile (product + docs + CLI run graph)
# Goal: show a user can compile across domains in one shot, then reuse the sr8_prompt.

USER
compile: design a local-only SROS v2 demo run that ingests a markdown doc into memory, runs a governed tool call via adapters, then emits receipts. Also generate a short docs page explaining the flow. Keep it CLI-oriented.

ASSISTANT (expected root)
<promptunit_package xmlns="https://srx.sros/schema/package/v2">
  <package_meta>...</package_meta>

  <replay_capsule>...</replay_capsule>

  <governance_receipt>
    <classification>GENERAL_BUILD</classification>
    <decision>ALLOW</decision>
  </governance_receipt>

  <sr8_prompts>
    <active><![CDATA[
<sr8_prompt id="SR8P.DEMO.SROSRun.v1" version="1.0.0" xmlns="https://sr8.sros/schema/prompt/v1">
  <role>SR8 Demo Compiler</role>

  <objective>
    Compile a local-only SROS v2 demo run (graph spec + CLI commands + receipts expectations) and a short docs page that explains the lifecycle.
  </objective>

  <inputs>
    <goal>Local-only SROS demo run: ingest markdown, governed adapter call, receipts emitted, plus docs page.</goal>
    <deliverables>
      <item>graph_spec</item>
      <item>cli_commands</item>
      <item>docs_page</item>
    </deliverables>
    <constraints>
      <item>Local-only. No web calls.</item>
      <item>Show governance gate before any adapter execution.</item>
      <item>Show memory ingest with provenance.</item>
      <item>Terminate with receipts list.</item>
    </constraints>
  </inputs>

  <manifest>
    <graph_spec>
      <nodes>
        <node id="N1" kind="INTAKE" />
        <node id="N2" kind="GOV_NODE" />
        <node id="N3" kind="MEM_INGEST" />
        <node id="N4" kind="GOV_TOOL" />
        <node id="N5" kind="ADAPTER_CALL" />
        <node id="N6" kind="MEM_WRITE" />
        <node id="N7" kind="MIRROR_POST" />
        <node id="N8" kind="RECEIPT_EMIT" />
      </nodes>
      <edges>
        <edge from="N1" to="N2"/>
        <edge from="N2" to="N3"/>
        <edge from="N3" to="N4"/>
        <edge from="N4" to="N5"/>
        <edge from="N5" to="N6"/>
        <edge from="N6" to="N7"/>
        <edge from="N7" to="N8"/>
      </edges>
    </graph_spec>

    <cli_commands>
      <cmd>sros init</cmd>
      <cmd>sros mem ingest --file ./knowledge/demo.md</cmd>
      <cmd>sros run --graph ./graphs/demo_run.srir</cmd>
      <cmd>sros receipts list --run latest</cmd>
    </cli_commands>

    <docs_page>
      <title>SROS v2 Demo Run (Local-only)</title>
      <sections>
        <section>High-level flow: Intake -> Compile -> Preflight -> Gov -> Mem -> Adapter -> Mirror -> Receipts</section>
        <section>What receipts you should see (node receipts + audit)</section>
      </sections>
    </docs_page>
  </manifest>

  <acceptance_tests>
    <test id="T1">Outputs include graph spec + CLI commands + docs page.</test>
    <test id="T2">Graph lifecycle includes explicit GOV gate before adapter call.</test>
    <test id="T3">No web dependency mentioned.</test>
  </acceptance_tests>
</sr8_prompt>
    ]]></active>
  </sr8_prompts>

  <compiler_run_report>...</compiler_run_report>
</promptunit_package>
