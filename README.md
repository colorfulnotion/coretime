# Proposal: Polkadot 2.0 CoreJam IDE - ChainIDE / Polkaholic.io Integration

- **Request**: 180K DOT
- **Date**: September 27, 2023 (DRAFT)
- **Team Name:** ChainIDE + Colorful Notion
- **Payment Addresses:** ChainIDE [15kdvsU1PnKCH9ShJ52cpiJmtmhSio4cPxwQK1pXgLrUGVSs](https://polkaholic.io/account/5GpLnYCwY13iqcSBLRycgZUd39ho2VWUKUCv9iqB8Fpx61QU?group=overview&chainfilters=all) + Colorful Notion [121Rs6fKm8nguHnvPfG1Cq3ctFuNAVZGRmghwkJwHpKxKjbx](https://polkaholic.io/account/DakP5k8XiY9DQbrCj23xdaUBEBxGrpJoenyB7bYDXWvtZbN?group=overview&chainfilters=all)
- **Beneficiaries**:  90K DOT Colorful Notion, 90K DOT ChainIDE 
- **Time period covered**: 9 months [5-6 FTE], pending CRJA working examples 

**Summary**: [Corejam](https://github.com/polkadot-fellows/RFCs/blob/dae162c8d4d2bf76796c78b74529bea86c37d013/text/0031-corejam.md) reimagines permissionless distributed computation with Work Packages that are paid for with [CoreTime](https://github.com/polkadot-fellows/RFCs/blob/main/text/0001-agile-coretime.md) credits.  To accelerate Corejam innovation and drive CoreTime revenue, this proposal aims to support 2 teams (ChainIDE and Colorful Notion) to: (1) deliver a **CoreJam IDE**; (2) extend Polkaholic.io to fully support CoreJam, integrated the CorePlay IDE of (1); (3) provide "Hello World" CoreJam templates to stimulate Polkadot developer activity.
 
**Background**: We build upon a Summer 2023 collaboration between [ChainIDE and Colorful Notion](https://github.com/use-inkubator/Ecosystem-Grants/blob/master/applications/chainide-polkaholic-integrated-wasm-contract-explorer-integration.md)  to support WASM Contract Development combining ChainIDE with Polkaholic.io.     With ChainIDE, just as in remix, anyone can compile their ink! WASM Contract or start with a WASM template (PSP22, PSP34, UniswapV2), post it to any Substrate chain with the contracts pallet (eg Astar or Rococo Contracts), and interact with it within the IDE.  At key touch points, developers can see their contract code deployed + stored, interact with contracts in ChainIDE with natural Polkaholic.io touchpoints (search/view by extrinsic hash, contract address, code hash, viewing contract source code + metadata, with ChainIDE-based verification backed by Parity Docker verifiable builds).   This work is funded under the [inkubator](https://use.ink/ubator/), where our Milestone 1 report has been submitted [here](https://github.com/use-inkubator/Grant-Milestone-Delivery/blob/baa71b51d5f97599f777b99206339cda96de86ab/deliveries/chainide-polkaholic-integrated-wasm-contract-explorer-integration-milestone_1.md).  See [here](https://www.dropbox.com/scl/fi/tf0jgxsmss5b52uk0nbw7/Astar-ChainIDE-M2-New.mp4?rlkey=ts3tpvzvxpbfg7wrl7f4va1yl&dl=0) for a video walkthrough.  See here for a preview as of Sept 2023: [ChainIDE WASM Contract Development Preview](https://staging-9589904a8a.chainide.com/s/dashboard/projects) 

As CoreJam _also_ uses WASM Code blobs in its CRJA MapReduce architecture, much of this summers efforts on WASM Contract IDE are natural to extend into a CoreJam IDE.  However, instead of compiling Rust into WASM Code Blobs stored on Astar/.. and referenced by Code Hashes in WASM Contract Addresses, a CoreJam IDE design compiles Rust into a family of new CoreJam objects stored on Polkadot/... in a new CRJA architecture.

#  Core Deliverable: Polkadot CoreJam IDE with ChainIDE + Polkaholic.io 
ChainIDE and Colorful Notion propose to work together to:

1.  [ChainIDE] Extend ChainIDE to support all CoreJam-enabled chains [Rococo or Westend, Kusama, Polkadot]  using Parity-developed [containers (similar to standardized verifiable builds)](https://github.com/paritytech/cargo-contract/pull/1148) that build Work Packages conforming to the CoreJam Collect-Refine-Join-Accumulate (CRJA) interface, and integrating with Polkaholic.io at natural touch points.  See **ChainIDE Details** below.
2. [Colorful Notion] Extend Polkaholic.io to support the CoreJam IDE and all CoreJam/CoreTime/CorePlay related innovations across the Polkadot ecosystem.  See **Polkaholic.io Details** below.
3. [Colorful Notion + ChainIDE] Develop 6 pedagogical CoreJam templates intended for developers to learn CRJA, experiment on Rococo and develop a path for them to be CoreTime customers.  See **CoreJam Templates** below.

| Number | Deliverable | Link | Notes |
| --- | --- | --- | --- |
| 0a. | License | [Polkaholic GNU GPL v3](https://github.com/colorfulnotion/polkaholic/blob/main/LICENSE) |   |
| 0b. | CoreJam IDE Video Walkthrough | Substantially in the same form as [video walkthough](https://www.dropbox.com/scl/fi/tf0jgxsmss5b52uk0nbw7/Astar-ChainIDE-M2-New.mp4?rlkey=ts3tpvzvxpbfg7wrl7f4va1yl&dl=0)  |   |
| 0c. | Technical Writeup | Substantially in the same form as [WASM Contract ChainIDE-Polkaholic Integration Milestone 1 Writeup](https://github.com/use-inkubator/Grant-Milestone-Delivery/pull/8) | |
| 0d. | Corejam Examples | https://github.com/colorfulnotion/corejam |
| 1. | Repository | https://github.com/colorfulnotion/polkaholic  | ChainIDE is only semi-open source. |
| 2. | CoreJam IDE integrated with Polkadot | Substantially in the same form as [WASM Contract IDE](https://staging-9589904a8a.chainide.com/s/dashboard/projects) | See ChainIDE Details below |
| 3. | Polkaholic 2.0 UI + API | [Polkaholic.io UI + API](https://polkaholic.io) augmented to support CoreJam  | See Polkaholic Details below |


## ChainIDE Details:

The ChainIDE team will extend the ChainIDE to support CoreJam in the following way:
- In ChainIDE backend, utilize images (to be provided by Parity) to compile Rust into CoreJam-deployable Blobs
- Add plugins and panels in ChainIDE for Rust to interface with the Storage API:
 - Provide an interactive user interface to configure and quickly start a local CoreJam development node (if possible)
  - Utilize wallet plugin for network connection, account management, and CodeJam code deployment interaction with Rococo/Westend, Kusama, Polkadot
  - Manage Wallet panel, manage network connection, account information
  - Select the CodeJam code to deploy to a CoreJam compatible chain in the deployment panel
  - Use interaction panel to interact with deployed CodeJam work class + work package
  - View Log viewer to see Work Results, linking to Polkaholic.io  
  - Support commonly used wallets: Polkadot, SubWallet, Math Wallet, and Talisman.
  - Support social sharing: github, zip and "Open in ChainIDE" url access  
  - Integrate Polkaholic CoreJam URLs --  url links (by network + workpackage hash, work class, work item, work report hash), iframes for corejam account activity (by network and address), work package DAG visualization + timeline (by network and work package hash)

## Polkaholic.io Details

CoreJam introduces the _WorkPackage_ as new primitive in blockchain technology to be manifested in CoreJam-enabled chains.  

* Colorful Notion will extend the [Polkaholic.io  UI](https://polkaholic.io) and [Polkaholic.io API](https://docs.polkaholic.io/#introduction)  will support URL parametric access to all CoreJam objects.  This will enable anyone to access data about CoreJam on-chain objects with simple  `{network}` and `{hash}` parameters, including ChainIDE.
	* We expect most of the CoreJam UI elements to follow the same pattern as with WASM Contract e.g. [WASM Code Hash](https://cdn.polkaholic.io/inkubator-m1/wasmcode-ui.png)  [WASM Contract](https://cdn.polkaholic.io/inkubator-m1/wasmcontract-ui.png),  [Extrinsic Hash](https://cdn.polkaholic.io/inkubator-m1/tx-ui.png) and so forth.  Two important exceptions are CoreJam DAG + CRJA Visualization, as noted below.
	* Any UI element should be exposable with Polkaholic APIs returning JSON.

 * _CoreJam DAG Visualization_.  A graph visualization package (e.g. d3.js) will be used to visualize the DAG of WorkPackages: the nodes of the DAG are work packages, edges in the DAG are prerequisites.  This DAG may be trivial with 1 prereq in [Hard-Ordered Queueing Alternative](https://github.com/polkadot-fellows/RFCs/blob/e4a117b0bc2d8c06a881c60cc8f0ca6655601dce/text/0027-corejam.md#hard-ordered-queueing-alternative) or arbitrarily complex as in [Soft Ordered Queueing Alternative](https://github.com/polkadot-fellows/RFCs/blob/e4a117b0bc2d8c06a881c60cc8f0ca6655601dce/text/0027-corejam.md#soft-ordered-queueing-alternative) as CoreJam evolves its design.  The UI should facilitate developer reasoning about this.
* _CRJA Visualization_. ([CRJA Processing stages of a Work Package](https://github.com/polkadot-fellows/RFCs/blob/e4a117b0bc2d8c06a881c60cc8f0ca6655601dce/text/0027-corejam.md#processing-stages-of-a-work-package)) happen at multiple block heights.  A distributed trace tool (e.g Jaeger) will be used to support the visualization of a work package's execution (authoring time `T`, map/refine at `T+r`, reduce/accumulate at `T+r+i` and availability `T+r+i+a`), keyed in by workPackageHash.
* _CoreJam IDE_. Using links and iframes from Polkaholic.io, any CoreJam IDE interface can readily incorporate Work Package DAG visualization, CRJA Processing Stages, the state of CoreJam on-chain objects, as well as CoreJam dashboards.
 
| UI/API URL | Deliverable|
| --- | --- |
| /workpackage/`{network}` | fetch/show work packages for { recently submitted, high weight usage (over last 24h) }, linking to work report, if available |
| /workpackage/`{network}`/`{workPackageHash}` | Show WorkPackage (see below) 
| /workitem/`{network}`/`{itemHash}` | Show work item, work class, and payload, and if available, show result (valid WorkOutput or error) | 
| /workreport/`{network}`/`{workreporthash}` | Show workpackagehash, context, core_index, and results; for each result, show signed attestations from the validator group
| /workclass/`{network}` | fetch/show { recently submitted, high weight usage (over last 24h) } workclasses |
| /workclass/`{network}`/`{workClass}` | fetch/show WeightRequirements of { recently submitted, high weight usage (over last 24h) } work packages | 
| /search/ | should accept any `workPackageHash`, `itemHash`, `workreporthash` and direct to the above |
| /corejam/`{address}` | See "To show CoreJam Account" below |


***Account CoreJam UI***  at https://polkaholic.io/corejam/`{address}`
* show any Instantaneous Coretime Credit (ICC), and if possible, enable developers to purchase Coretime credit; 
* show any work packages associated with the account and a summary of any recent activity
* show requested / unrequested storage, where the address is the depositor

***Work Package UI*** https://polkaholic.io/workpackage/`{network}`/`{workPackageHash}` 
 * show the Work Package authorization, context (header_hash, prerequisites), and items;  for each item, show class + payload + item_hash, and its associated result (valid WorkOutput or error) of CRJA computation, if completed
*  show DAG visualization of prereqs and what the work package is a prereq of; users should be able to click on neighboring DAG elements and arrive at other work package pages
- show the work report for the work package, if available
- show data availability status

### CoreJam Developer dashboards 

The Polkaholic.io CoreJam developer dashboard will be built using [Apache Superset](https://superset.apache.org/), a popular open-source modern data exploration and visualization platform that is hosted at https://analytics.polkaholic.io  This can be connected to Colorful Notion's [substrate-etl](https://github.com/colorfulnotion/substrate-etl) BigQuery as well as the Polkaholic MySQL replicas.    Many dashboards can be built in Superset very rapidly (with no "front end engineering").  For this deliverable we propose to build two core dashboards, with `{network}` and `{developerAddress}` URL parameters:

|Function|URL|Example|
|------|----|----|
| CoreJam Activity for one network, across all developers |  Similar to [WASM Contract - All Developers](https://analytics.polkaholic.io/superset/dashboard/20/?network=shibuya&standalone=2) [screenshot](https://cdn.polkaholic.io/inkubator-m1/dashboard20.png) |
| CoreJam Activity for specific developer on one network |  Similar to [WASM Contract - Specific Developer](https://analytics.polkaholic.io/superset/dashboard/57/?network=shibuya&developer=afAEAGz4MVRQjkqUuaUTCU9nTPHruE5xfvazKzPs4kndwso&standalone=2)  [screenshot](https://cdn.polkaholic.io/inkubator-m1/dashboard57.png) |

These dashboards will be integrated into CoreJam IDE similar to the WASM Contract IDE.  Other dashboards can be built rapidly and used to build Polkadot analytics specific to CoreJam.

### substrate-etl BigQuery Public Datasets

Colorful Notion expects to index CoreJam objects from Polkaholic.io in [Google BigQuery Public Datasets](https://twitter.com/Polkadot/status/1707052392712212676).
It is expected that many analytical operations on weight, developer address can be done within BigQuery (e.g by Parity Data).
This public index can be incorporated by public dashboard systems (Dune, Nansen), Parity Data and the [Polkadot Data Alliance](https://docs.google.com/document/d/1fA5ARHy-frzgZC66rniKZ5o7CSbDvCTkS--kWaMzuMs/edit#heading=h.foftxwdr3st2) who can analyze CoreJam developer adoption, CoreTime usage, and support growth the Polkadot 2.0 ecosystem generally. 

## CoreJam Templates

CoreJam promises to stimulate an new generation of developers to join the Polkadot ecosystem with the CoreJam IDE + CRJA programming interface.  Developers learn new programming concepts with concise examples, such as "word count" in [MapReduce](https://saturncloud.io/blog/mapreduce-word-count-in-hadoop-finding-the-highest-frequency-word/) and  [ERC20 examples](https://solidity-by-example.org/app/erc20/) in Solidity / EVM Contracts.  ChainIDE assists new EVM Developers with EVM Templates and this summer, incorporated WASM Contract Templates for flipper, PSP22,  PSP34 and Uniswapv2 into the Astar IDE.    

The CoreJam IDE can be used to provide developers with representative CoreJam code templates (written in Rust, compiling to Work Package blobs) that illustrate the key aspects of the CRJA architecture:
* use of `refine` `accumulate` and `prune` hooks 
```
fn refine(payload: WorkPayload, authorization: Authorization, auth_id: Option<AuthId>, context: Context, package_hash: WorkPackageHash) -> WorkOutput;
fn accumulate(results: Vec<(Authorization, Vec<(ItemHash, WorkResult)>)>);
fn prune(outputs: Vec<WorkOutput>) -> Vec<usize>;
```
* use of the Storage API, specifically the Work Class Trie interface
```
fn get_work_storage(key: &[u8]) -> Result<Vec<u8>>;
fn get_work_storage_len(key: &[u8]);
fn checkpoint() -> Weight;
fn weight_remaining() -> Weight;
fn set_work_storage(key: &[u8], value: &[u8]) -> Result<(), ()>;
fn remove_work_storage(key: &[u8]);
```

A basic set of 5-6 representative CoreJam code templates that have pedagogical simplicity will be developed by Colorful Notion and onboarded to the CoreJam IDE by ChainIDE team:

* 2 demonstrations of the Collect-Refine vs Join-Accumulate in `refine` and `accumulate` , one close to flipper / word count and another in higher complexity
* 2 demonstrations of the [CorePlay/Actor model](https://github.com/polkadot-fellows/RFCs/blob/ba59c9f4675e072603dd6a6c6dccdcd9c7d1524a/text/coreplay.md) showing Actor progression in CRJA
* 1-2 demonstrations of the importance of `prune`, outside the CorePlay/Actor progress, of higher complexity than the above

These will be added to this repo.  These are not intended to
demonstrate complexity but to get developers learning and
experimenting with the Work Package / CRJA flow, and should be
suitable for the [Polkadot Blockchain
Academy](https://forum.polkadot.network/t/opening-polkadot-blockchain-academy-content-to-the-world/3904)
-- none should be more than 300 lines of Rust code, ideally less than
100-200, and be accessible to people learning Rust.  The broader
community is welcome to contribute CoreJam templates, simply by
submitting a PR here to this repo.  

An "Open in ChainIDE" functionality in Polkaholic.io, coupled with the
ability to upload verifiable CoreJam code, can be used to make for
CoreJam developer experience match the "Try on Remix" familiar to EVM
Solidity developers.  If Polkadot has both WASM Contract and EVM
Contract functionality to support CoreJam WASM + EVM _interpretation_
this social mechanism can adjusted to cover WASM Contracts (ink!),
EVM Contracts (Solidity), other VMs as well as CoreJam CRJA Rust code
in a hybrid multi-VM aware IDE.  It remains to be seen if Polkadot 2.0 will
incorporate EVM+WASM contract functionality similar to that of Astar and Moonbeam.

## Team :busts_in_silhouette:
### Key Team members
- Colorful Notion: Sourabh Niyogi  + Michael Chung
- ChainIDE: 
  - Xiao Wu, Founder of ChainIDE: https://www.linkedin.com/in/%E5%95%B8-%E5%90%B4-4727237a/?locale=en_US
  - Tim Zhang,  Co-founder and CTO of ChainIDE, former Amazon star employee: https://www.linkedin.com/in/timzmatrixlabs/
  - Alvin Sun, Chief Scientific Officer, CBC(Canadian Blockchain Consortium) Web3 Committee Member: https://www.linkedin.com/in/xinyao-alvin-sun/
  - Jerry Zhang, Product Manager: https://www.linkedin.com/in/jerry-zhang-5a8820220/
  - Leon Liu, Project Managerhttps://www.linkedin.com/in/leon-liu-b4a379117/


### Contact
* **Contact Name:** Sourabh Niyogi
* **Contact Email:** sourabh@colorfulnotion.com
* **Website** https://polkaholic.io/

### Legal Structure

Colorful Notion:
- **Registered Address:** 55 E Third Ave San Mateo, CA 94401
- **Registered Legal Entity:** Colorful Notion, Inc.

Colorful Notion is a multichain analytics company focused on L1/L2
Substrate+EVM Chains and bridges.  Founded in 2021, our approach has
been heavily guided by Substrate's numerous key innovations (XCM,
WASM+EVM) which we embed in our key projects Polkaholic.io, XCMGAR and
Substrate-etl.

ChainIDE:
- **Registered Address:** Vistra Corporate Services Centre, Wickhams Cay II, Road Town, Tortola, VG1110, British Virgin Islands
- **Registered Legal Entity:** Matrix Global Inc.

ChainIDE is a multi-chain tooling platform that provides one-stop development services for blockchain developers. By providing cloud-based user experiences, ChainIDE enables users to immediately begin developing decentralized applications with no configuration, without any pre-installation or requirements on their local system. It is designed to streamline the development process by providing a user-friendly interface and a suite of tools and services to help developers write, test, and deploy smart contracts and dApps.



### Team's experience

ChainIDE was founded in 2017. Our team has been working in the blockchain field for more than five years. The core members have a combined experience of more than ten years in computing science and more than five years in blockchain development experiments. Additionally, we have over 30 product developers and a research and development team comprising ten senior engineers to ensure our services and products' effective and high-quality delivery.

Colorful Notion is led by Sourabh Niyogi and Michael Chung who have been active in blockchain engineering since 2017.  Key engineers Sourabh Niyogi and Michael Chung have developed Polkaholic.io since Fall 2021. Prior to building Polkaholic.io, Sourabh and Michael worked in decentralized social networking protocol development + privacy-preserving contact tracing (Wolk), mobile advertising real-time bidding algorithm design and analytics
(CrossChannel/MdotM).   Sourabh has founded social + web advertising startups (Social Media Networks) in the SF Bay and spent time doing computational cognitive science and machine vision research at MIT. Michael hails from UC Berkeley.  In the last year, Colorful Notion has worked closely with Parity Data, many parachains with substrate-etl, XCM GAR and polkaholic.io.  

### Team Code Repos

[Colorful Notion](https://github.com/colorfulnotion)
* [polkaholic](https://github.com/colorfulnotion/polkaholic)
* [substrate-etl](https://github.com/colorfulnotion/substrate-etl)

## Development Status :open_book:

CoreJam is an active Work-In-Progress led by Parity/Polkadot founder Gavin Wood, Robert Habermeier, Bastian Köcher and the Parity engineering team.  While most of the components have already been developed in Polkadot 1.0 (Polkadot's Data availability and Parachain ), we expect much of Fall 2023 will involve Parity engineering putting the Work Package concept together into the key `refine` `accumulate` and `prune` hook points from this foundation.  We imagine a "Hello World" example equivalent of WASM Contract "flipper" can be provided in a Docker container similar to the cargo-contract verify.  Thereafter, this proposal depends on Parity Engineers being able to support both teams with CoreJam compilation and debugging.   

Core Deliverables requires collaborative but asynchronous development between the 2 teams and depends heavily on Parity rollout of  CoreJam.    We anticipate full-time development to commence as soon as a Corejam Local PoC exists, with involvement of 2.5-3 FTE (on average) from Colorful Notion and 2.5-3 FTE from ChainIDE over 6 months.  As CoreJam is a work in progress, a 1-2 month period of planning and design would be appropiate in Fall 2023 and a 1-2 month period of developer feedback in Summer 2024.  

We hope the following timeline can be realistic for CoreJam deployment:

| {network} | Relay Chain | Timing |  
|----|---|---|
| `rococo` / `westend` | Rococo / Westend | Winter/Spring 2024 |
| `kusama` | Kusama | Spring/Summer 2024 | 
| `polkadot` | Polkadot | Summer/Fall 2024 |

With a developer preview edition on rococo and kusama in Spring/Summer 2024, we expect to publish additional Corejam Templates and get a broad range of feedback on how to improve CoreJam IDE and Polkaholic.io.  

With short-term and long-term FTE support from the Polkadot Treasury, both ChainIDE and Colorful Notion hope support the Polkadot ecosystem with integrated multi-chain products and services.  We believe 2024 is an important year to demonstrate the Instantaneous CoreTime Credit (ICC) business model and are excited to help CoreJam come to reality and can work with a sense of urgency.
  
## Additional Information :heavy_plus_sign:

Both teams expect to continue working on WASM Contract Development in
the inkubator program with 0.5-1 FTE amidst this process, but may
prioritize this project lower or higher based on curator feedback as
well as the CoreJam architects.  

 

