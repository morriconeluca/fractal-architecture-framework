# Fractal Architecture Framework (FAF)

FAF governs TypeScript codebase architecture through directory hierarchy and file naming.

- **Declaration**: Architect-stated constraint integrating FAF conventions. Declarations must be complete, compatible with FAF taxonomy, and never derogate from any FAF norm.
- **Conformance**: Prescriptions marked _recommended_ are non-binding recommendations; every other prescription is a mandatory **norm**. Conformance requires satisfying all norms and all codebase Declarations.

## 1. Principles

A **Fractal Tree** is a codebase subtree rooted at an origin directory identified by a Declaration.

- **Fractal Decomposition**: Model the system via one or more disjoint Fractal Trees (sharing no files or directories), each an autonomous architectural space dedicated to a specific problem. Files and directories outside all Fractal Trees fall outside FAF taxonomy (governed only at the tree frontier). Within each Fractal Tree, decompose recursively: at every scale, solve each cohesive sub-problem in a dedicated logical unit under a self-similar organizational structure.
- **Semantic Form**: File and directory hierarchy and naming must reveal every logical unit's architectural purpose, as they directly determine encapsulation boundaries and permitted dependencies.
- **Proportionality**: Decomposition depth and granularity must match the complexity of the problem solved.

## 2. Foundations

- **Dependency Graph**: Within a Fractal Tree, the directed graph whose vertices are its Logical Nodes and whose edges connect each source Logical Node to each directly imported target Logical Node. An **import** is any static reference requiring resolution of another codebase file (e.g., `import`, `import type`, `export … from`, `import()` with a literal specifier, `require`, stylesheet `@import` and `url()`).
- **Logical Nodes vs. Foreign Nodes**: Every file in a Fractal Tree is exclusively one:
  - **Logical Node**: Dependency Graph vertex permitted to import, export, or be imported.
  - **Foreign Node**: File identified by a Declaration as excluded from the Dependency Graph. Forbidden from any incoming or outgoing import with any codebase file. No file is a Foreign Node without a Declaration covering it, regardless of extension or content.
- **Asset**: Logical Node whose content is not TypeScript or JavaScript code (e.g., stylesheets, fonts, images, JSON).
- **Symbol**: Each root-scope declaration in a non-Asset Logical Node, in value or type space, exported or unexported (`const`, `let`, `var`, `function`, `class`, `enum`, `type`, `interface`, `namespace`).
  - **Distinct Symbols**: each binding in multi-variable or destructured declarations; each homonymous declaration subject to declaration merging; each declaration initialized with an imported binding.
  - **Single Symbol**: all overload signatures with the implementation of the same function; an anonymous `export default`.
  - Import declarations introduce no Symbols.
- **Role**: Semantic label qualifying a Logical Node's architectural responsibility. For one or more Fractal Trees, a **catalog Declaration** establishes a closed Role set, distinguishes **Sub-Graph Roles** from ordinary Roles, and for each ordinary Role defines its Rank, distinct exact Category name, Category form (`Fragments` or `Category Nodes`), whether multiple Symbols are permitted, and any **implicit extensions** (Asset extensions bound to a single Role; first segment must match no catalog Role name).
  - With `<name>` as the initial segment (containing no `.`) and `<extension>` as the final segment or a trailing segment sequence matching an implicit extension (e.g., `.tar.gz`), a Logical Node's Role (except Root Nodes) is:
    - **Explicit**: `<name>.<role>.<extension>` with `<role>` in the catalog (e.g., `button.component.tsx`, `button.module.css`).
    - **Implicit**: Asset named `<name>.<extension>` where `<extension>` is an implicit extension of that Role (e.g., `theme.css`, `inter.woff2`).
    - **Absent**: matches neither form (e.g., `index.ts`, `example.util.spec.ts`).
- **Execution Sub-Graphs and Sub-Graph Nodes**: Each execution context (e.g., runtime, build, test, Storybook) operates on an **Execution Sub-Graph** reachable from its entry Logical Nodes. A **Sub-Graph Role** (e.g., `spec`, `story`) is reserved for entry Logical Nodes of dedicated Execution Sub-Graphs and attributed exclusively in explicit form. A **Sub-Graph Node** is a Logical Node with a Sub-Graph Role and must not be imported by any Logical Node.
- **Logical Domain**: Every directory in a Fractal Tree, forming a transitive semantic boundary over all Logical Domains, Logical Nodes, and Foreign Nodes in its subtree:
  - **Functional**: isolates a single logical unit (`Fragment`, `Root Fragment`).
  - **Organizational**: does not constitute a single logical unit (`Category`, `Sub-Category`, `Path Sub-Category`, `Layer`, `Root Layer`, `Fractal Branch`, `Foreign Domain`).
- **Horizontal Hierarchy**: Declaration assigning natural-number **Ranks** ($0, 1, 2, \dots$) to a set of direct-child siblings of one parent Logical Domain — either Logical Nodes or Logical Domains, never mixed.
  - Authorizes dependencies exclusively within its set, from Rank $N$ to strictly lower Rank $M$ ($M < N$).
  - Multiple Horizontal Hierarchies under one parent may coexist only on disjoint sets of direct children; Ranks from distinct hierarchies are not comparable.
  - Between Logical Domains, a Declaration targets a single parent Logical Domain and orders direct children actually present under it across at least two distinct Ranks — except on Sub-Categories, which also admit **Fractal-Tree-wide models** partitioning Sub-Category names (distinct from all catalog Category names) across at least two distinct Ranks and instantiating a hierarchy wherever those direct-child Sub-Categories appear.
  - Permitted exclusively on: (1) direct-child Logical Nodes of a Fragment, (2) Root Nodes of a Root Fragment (at most one hierarchy per Root Fragment), (3) non-private sibling Categories, (4) sibling Sub-Categories excluding Path Sub-Categories (including inside a Private Category), or (5) sibling Layers (including Sub-Layers). Forbidden on all other sets (including sibling Fragments, sibling Category Nodes, sibling Private Categories, and Path Sub-Categories). Membership does not alter Logical Domain classification.
- **Naming**: Unless prescribed otherwise by external technology contracts or FAF, file and directory identifiers use `kebab-case` with FAF syntactic delimiters. Fractal Tree origin directories, child Root Fragments, Root Nodes, Foreign Domains, and Foreign Nodes have free naming. For all other Logical Domains, a leading `_` marks **Organizational** domains, whereas **Functional** domains omit `_`.

## 3. Dependency Graph Laws

- **Directed Acyclic Graph (DAG)**: The Dependency Graph must be acyclic.
- **Peer Separation**: Any dependency between Logical Nodes in subtrees of sibling Logical Domains, or between sibling Logical Nodes in the same Logical Domain, is forbidden unless authorized by an applicable Horizontal Hierarchy or specific Logical Domain visibility rules.
- **Symbol Uniqueness**: Every non-Asset, non-Sub-Graph Logical Node with an explicit Role defines at most one Symbol coherent with its Role, unless the catalog Declaration permits multiple Symbols for that Role; additional Symbols each require a dedicated Logical Node.
  - _Recommended_: permit multiple Symbols only for Roles whose nature entails correlated or auxiliary declarations (e.g., `constant`, `mock`, `recipe`, `schema`, `styled`, `type`, `util`).
  - Where multiple Symbols are permitted, only mutually inseparable Symbols within the same responsibility may coexist; autonomous Symbols require distinct Logical Nodes or dedicated Sub-Fragments. _Recommended_: do not bypass separation of responsibilities by bundling distinct domain logic or cases into one Symbol.
  - Mechanical derivability does not imply architectural identity: Symbols serving distinct responsibilities require distinct Logical Nodes with distinct Roles (e.g., a validation schema and its inferred static type).
- **No Re-Export**: Every Logical Node with an explicit Role is forbidden from re-exporting imported Symbols.

## 4. Logical Domains

Every Logical Domain may directly contain Foreign Nodes and Foreign Domains; each subsection below specifies exhaustive placement and remaining direct children.

### 4.1. Fragments

Functional Logical Domain (`kebab-case`, no `_`) implementing a cohesive, self-contained logical unit (e.g., `button/`, `use-example/`, `get-todos/`) with an imposed **Role of the Fragment**.

- **Placement and Nesting**: Placed exclusively as a direct child of a Category (including Private Category), Sub-Category, or Path Sub-Category. May enclose internal **Sub-Fragments** in its subtree exclusively via intermediate Organizational Logical Domains; its nearest enclosing Fragment (with no interposed Fragments) is its **Parent Fragment**.
- **Direct Children**: Private Categories, at most one Fractal Branch, and direct-child Logical Nodes (each explicit Role appears at most once) of exclusively three kinds:
  - **Fragment Nodes**: Explicit non-Sub-Graph Role, named `<fragment>.<role>.<extension>` (`<fragment>` matching the Fragment directory name). Includes a mandatory **Master Node** — the unique Fragment Node matching the Fragment's Role — which must define a single root-scope Symbol and export it, even when the catalog permits multiple Symbols for that Role. Only higher-Rank direct-child Logical Nodes of the same Fragment may import its Fragment Nodes; importing them from outside the Fragment or from its subtrees is forbidden.
  - **Access Node** (`index.ts`): Mandatory unique Logical Node with absent Role; exclusive public interface of the Fragment. Must re-export the Master Node's Symbol, may selectively re-export other Fragment Nodes' Symbols of the same Fragment, must not define its own Symbols, and must not import or re-export anything other than Symbols defined by Fragment Nodes of the same Fragment.
  - **Sub-Graph Nodes**: Explicit Sub-Graph Role, named `<fragment>.<role>.<extension>`, consuming or observing the Fragment's Fragment Nodes for dedicated Execution Sub-Graphs.
- **Internal Horizontal Hierarchy**: Each Fragment Node takes its catalog Role Rank; `index.ts` and Sub-Graph Nodes jointly occupy `maxCatalogRank + 1` (neither may import the other). Every non-Master Fragment Node must have a Rank strictly lower than the Master Node's Rank.
- **Role Catalog Design** _(recommended)_:
  - Define only Roles needed to distinguish recurring domain responsibilities from auxiliary ones — avoiding both collapsing primary domain units into a generic auxiliary Role (hiding their nature and preventing Fragments from composing Fragment Nodes of that Role) and introducing speculative, single-unit, purely infrastructural, or syntax/class-mirroring Roles (Role expresses responsibility and Rank; unit-specific purpose belongs in the Fragment or Logical Node name).
  - Assign a strictly lower Rank solely when Fragment Nodes of those Roles can coexist in one Fragment with direct or transitive dependency; assign equal Rank to non-interacting auxiliary Roles; align primary Master-Node-only Roles at the catalog's top Rank so distinct primary responsibilities compose via Access Nodes.
  - Split conceptual/technical families across contractual boundaries (source Fragment Nodes from which contracts like `type` derive vs. consumers depending on those contracts) to prevent intra-Fragment cycles (e.g., `constant` < `type` < `config`/`mock`; `style`/`module`/`recipe` < `type` < `styled`; `schema`/`contract` < `type` < `handler`/`route`).
- **Role Reference Model** _(illustrative; active only as adopted by Declaration)_:
  - **Rank 0** _(Static Primitives)_: `constant`, `font`, `image`
  - **Rank 1** _(Declarative Definitions)_: `markup`, `model`, `module` (CSS Modules), `style` (CSS)
  - **Rank 2** _(Style Variants & Schemas)_: `recipe`, `schema`
  - **Rank 3** _(Interface Contracts)_: `contract`
  - **Rank 4** _(Static Types)_: `type`
  - **Rank 5** _(Typed Production Constructs)_: `config`, `error`, `styled`
  - **Rank 6** _(Simulation Data)_: `mock`
  - **Rank 7** _(Pure Functional Processing)_: `util`
  - **Rank 8** _(Creational Functions)_: `factory`
  - **Rank 9** _(Preconfigured Instances)_: `instance`
  - **Rank 10** _(External Data & Service Connectors)_: `api`, `repository`
  - **Rank 11** _(Local Coordination)_: `handler`, `hook`
  - **Rank 12** _(Application Coordination)_: `component`, `context`, `job`, `layout`, `middleware`, `page`, `route`, `router`, `service`, `store`
  - **Rank 13** _(Top Rank)_: `index.ts` (Access Node), `spec` (Sub-Graph), `story` (Sub-Graph)

### 4.2. Root Fragments

Functional Logical Domain with free naming (e.g., `src/`, `app/`) acting as an external tool frontier (e.g., bundler entry points, file-system routing) or surfacing primary functional partitions directly at the Fractal Tree root without hiding them under value-less intermediate domains. _Recommended_: omit the `_` prefix.

- **Placement and Identification**: Placed exclusively as a Fractal Tree origin or direct child of another Root Fragment; identified (along with its direct-child Root Fragments) exclusively by Declaration. Has no Master Node and no Access Node.
- **Direct Children and Root Nodes**: Declared child Root Fragments, Private Categories, at most one Fractal Branch, and **Root Nodes** (all direct-child Logical Nodes, exhaustively enumerated by Declaration; every other direct-child file must be declared a Foreign Node). Root Nodes have free naming, absent Role, and no Fragment/Access/Sub-Graph qualification regardless of filename (Role Ranks, Symbol Uniqueness, and No Re-Export do not apply).
- **Root Node Dependencies**: Within the same Fractal Tree, a Root Node must not be imported by any Logical Node other than another Root Node. Dependencies between Root Nodes are forbidden unless authorized by:
  - **Same Root Fragment**: a single declared Horizontal Hierarchy ordering its Root Nodes.
  - **Distinct Root Fragments (same Fractal Tree)**: a Declaration authorizing source Root Nodes of a source Root Fragment to target Root Nodes of other Root Fragments (multiple sources/targets authorize every source–target pair; target membership is unchanged; authorizations do not require imports to exist and grant neither reverse nor transitive edges).

### 4.3. Categories

Organizational Logical Domain (`_` prefix, `kebab-case`; _recommended_: plural name) classifying homogeneous units sharing one Role (e.g., `_components/`, `_hooks/`, `_styles/`, `_types/`, `_utils/`).

- **Catalog Mapping and Placement**: Unless overridden by Path Sub-Category rules or a Foreign Domain Declaration, any directory in a Fractal Tree matching a catalog Category name is a Category and imposes its Role (declaring a Role's Category name does not require that Category to exist). Placed exclusively as a direct child of a Root Layer, Layer, or Fractal Branch (non-private), or of a Fragment or Root Fragment (**Private Category**). Cannot be a direct child of a Category or Sub-Category, nor a sibling of Sub-Categories or Layers. Forbids Access Nodes (`index.ts`); classified units are imported individually.
- **Category Form and Category Nodes**: A **Category Node** is a Logical Node without Fragment encapsulation classified by a Category (or Sub-Category) matching its Role. Per Role across the entire Fractal Tree, the catalog Declaration establishes one mutually exclusive form:
  - **Category of Fragments**: classifies Fragments whose Role matches the Category's Role.
  - **Category of Category Nodes**: classifies Category Nodes with explicit (`_types/user.type.ts`) or implicit (`_styles/theme.css`) Role. Implicit Roles are permitted exclusively as Category Nodes; any Role with implicit extensions must adopt `Category Nodes` form tree-wide. Forbids Fragment encapsulation and dedicated Sub-Graph Nodes for units of that Role, while keeping the Role allowed in explicit form as non-Master Fragment Nodes. _Recommended_: use `Category Nodes` form when units require neither Fragment Node/Sub-Fragment composition nor dedicated Sub-Graph Nodes (e.g., `constant`, `model`, `type`, `config`, `mock`), and `Fragments` form otherwise.
  - Direct-child Logical Nodes with absent Role or a different Role are forbidden.
- **Sub-Categories**: Organizational direct children (`_` prefix, `kebab-case`; _recommended_: plural name) of a Category (**Parent Category** of the chain) or another Sub-Category whose names match no catalog Category name (unless Mimetic Path Structure, Fractal Branch, or Foreign Domain). Propagate unchanged the Parent Category's Role and form; forbid Access Nodes. Within each Category and Sub-Category (aside from an optional Fractal Branch), branching into Sub-Categories and directly containing Fragments or Category Nodes are mutually exclusive.
- **Private Categories**: Any Category placed as a direct child of a Fragment or Root Fragment.
  - From outside the Private Category, its classified units may be imported exclusively by direct-child Logical Nodes of its parent Logical Domain — in a Fragment: direct-child Fragment Nodes and Sub-Graph Nodes (excluding `index.ts`); in a Root Fragment: direct-child Root Nodes — subject to inner encapsulation boundaries.
  - **Unidirectional**: no Logical Node in a Private Category's subtree may import direct-child Logical Nodes of the parent Logical Domain.
- **Sub-Category Reference Models** _(illustrative tree-wide models; active only if declared)_:
  - **Atomic Design** (UI components): Rank 0 `_atoms`, Rank 1 `_molecules`, Rank 2 `_organisms`, Rank 3 `_templates` (_recommended_: classify `pages` via a sibling Category with a distinct Role, e.g., `_pages/` with Role `page`, rather than as a component Sub-Category).
  - **Systemic Design** (logical, algorithmic, or infrastructural domains): Rank 0 `_primitives`, Rank 1 `_compounds`, Rank 2 `_aggregates`, Rank 3 `_systems`, Rank 4 `_ecosystems`.
- **Mimetic Path Structure**: Declaration on a Category of Fragments (**Parent Category**; forbidden on a Category of Category Nodes) mapping an external hierarchical address space (e.g., HTTP/REST endpoints, programmatic UI routes, CLI commands, event topics, RPC/IPC namespaces) within Category taxonomy:
  - **Path Sub-Categories**: Organizational direct children (other than Fractal Branch or Foreign Domains) of the Parent Category or another Path Sub-Category; no Access Node; map 1-to-1 to address segments and propagate unchanged the Parent Category's Role (overriding catalog Category-name matching):
    - **Static**: `_<segment>/` (`<segment>` in `kebab-case`, exempt from plural naming).
    - **Dynamic**: `_[<parameter>]/` (`<parameter>` in `kebab-case`).
  - **Path Fragments**: Fragments (taking the Parent Category's Role) placed as direct children of the Parent Category (root coordinate) or of a Path Sub-Category (coordinate path), implementing the unit at that coordinate without replacing segment Path Sub-Categories. Named per one mutually exclusive declared mode on the Parent Category:
    - **With Action Catalog**: closed **Action Catalog** declared on the Parent Category; named `<action>-<target>` in `kebab-case` (`<action>` in Action Catalog, `<target>` identifying the entity/resource; overlapping compound `kebab-case` actions resolve by longest matching prefix in the Action Catalog).
    - **Without Action Catalog**: named `<target>` in `kebab-case`.
  - Direct children of Parent Category or Path Sub-Category: Path Sub-Categories and Path Fragments may coexist; at most one Fractal Branch; Category Nodes forbidden.

### 4.4. Layers

Organizational Logical Domain (`_` prefix, `kebab-case`) defining a cross-Role architectural abstraction plane (e.g., `_domain/`, `_network/`, `_state/`, `_ui/`), bound to and imposing no Role, with no predefined reference models.

- **Placement and Direct Children**: Placed exclusively as a direct child of a Root Layer, Fractal Branch, or another Layer (**Sub-Layer**, governed by identical rules). Cannot be a sibling of a Category or Sub-Category. Direct children: at most one Fractal Branch, and exclusively one of non-private Categories or Sub-Layers.

### 4.5. Root Layers

Organizational Logical Domain with free naming (e.g., `src/`, `lib/`) structuring a Fractal Tree origin directly into organizational partitions, bound to and imposing no Role.

- **Placement and Direct Children**: Identified exclusively by Declaration and placed exclusively as a Fractal Tree origin (every Fractal Tree origin is either a Root Fragment or a Root Layer). Direct children: at most one Fractal Branch, and exclusively one of non-private Categories or Layers.

### 4.6. Fractal Branches

Organizational Logical Domain encapsulating units and implementation details shared across subtrees of its parent Logical Domain.

- **Naming, Placement, and Direct Children**: Reserved name `_<scope>@shared/`, where `<scope>` equals the parent directory name stripped of any leading `_` (hence at most one direct-child Fractal Branch per Logical Domain). Placed exclusively as a direct child of a Root Fragment, Root Layer, Fragment, Category (including Private Category), Sub-Category, Path Sub-Category, or Layer — never as a direct child of another Fractal Branch or of a Foreign Domain. Direct children: exclusively one of non-private Categories or Layers.
- **Visibility and Unidirectionality**:
  - **Authorized consumers**: From outside the Fractal Branch, access is permitted exclusively to Logical Nodes in the subtree of the Fractal Branch's parent Logical Domain, excluding the parent's `index.ts` when the parent is a Fragment.
  - **Encapsulation boundary**: Authorized consumers may import exclusively units classified by direct-child Categories of the Fractal Branch or of Layers/Sub-Layers inside the Fractal Branch, including their Sub-Categories and Path Sub-Categories (Fragment -> `index.ts`; Category Node -> Category Node itself). Visibility does not cross into Fragments, Private Categories, or nested Fractal Branches.
  - **Unidirectionality**: No Logical Node in a Fractal Branch's subtree may depend, directly or indirectly, on direct-child Logical Nodes of the Fractal Branch's parent Logical Domain or on any Logical Node in the other subtrees of that parent Logical Domain.

### 4.7. Foreign Domains

Organizational Logical Domain with free naming (_recommended_: `_` prefix unless externally constrained) identified by Declaration to isolate Foreign Nodes (e.g., `_tooling/`).

- **Placement and Scope**: Direct child of any Logical Domain; admits exclusively Foreign Nodes and nested Foreign Domains. The Declaration extends automatically to its entire subtree without individual enumeration and overrides catalog Category-name matching at that path without affecting other occurrences of the name.
- **Standalone Foreign Nodes**: Foreign Nodes outside Foreign Domains require individual or file-family Declarations defined by an explicit criterion and application scope.

### 4.8. Classification Completeness

- Declarations and FAF conventions must assign every file in a Fractal Tree uniquely as a Logical Node or Foreign Node, and every directory uniquely as one Logical Domain kind; any unclassified or ambiguously classified file or directory is a violation.
- In containers eligible to host Layers (`Root Layer`, `Layer`/`Sub-Layer`, `Fractal Branch`), Organizational (`_`-prefixed) directories not classified as Categories, Fractal Branches, or Foreign Domains are Layers.

## 5. Fractal Tree Frontier and External Relations

- **Public Surface**: Exclusive interface of a Fractal Tree toward external consumers:
  - **Root Fragment origin**: zero, one, or more Root Nodes of the Fractal Tree designated by Declaration.
  - **Root Layer origin**: structurally determined without extra Declaration, comprising exclusively units classified by direct-child Categories of the Root Layer or of Layers/Sub-Layers inside the Root Layer, including their Sub-Categories and Path Sub-Categories (Fragment -> `index.ts`; Category Node -> itself), without crossing into Fragments, Private Categories, or Fractal Branches (including the origin Root Layer's own Fractal Branch).
  - **Frontier invariants**: From outside the Fractal Tree, importing Logical Nodes outside its Public Surface is forbidden (**external opacity**). Exposure in the Public Surface does not alter intra-tree visibility constraints (**internal invariance**).
- **Inter-Tree Relations**: Fractal Trees are isolated by default. Any dependency from a source Fractal Tree to a distinct target Fractal Tree requires a Declaration authorizing `source -> target`. When authorized, any Logical Node of the source Fractal Tree — excluding Fragment Access Nodes — may import exclusively Logical Nodes in the target's Public Surface, subject to re-export prohibitions on the importing node. Inter-tree dependencies must form a **DAG**.
- **External Local Codebase Files** _(modular codebase files outside all Fractal Trees, distinct from external library packages)_:
  - **Outgoing**: Logical Nodes of a Fractal Tree (excluding Fragment Access Nodes) must not import codebase files outside all Fractal Trees unless a Declaration identifies both permitted external paths and authorized Logical Nodes or Logical Domains.
  - **Induced inter-tree dependencies**: Any import path from a Logical Node of one Fractal Tree to a Logical Node of another Fractal Tree traversing exclusively files outside all Fractal Trees constitutes a dependency between those two Fractal Trees.
  - **No re-entry**: No import path traversing files outside all Fractal Trees may re-enter the originating Fractal Tree.
- **Path Aliases** _(optional)_:
  - **Anchoring**: Importing via Path Alias a Logical Node in the same Fractal Tree as the importing Logical Node requires a Path Alias where each base target is a Fractal Branch of that Fractal Tree (e.g., `#_src@shared/*`).
  - **Invariance**: Path Aliases neither modify the Dependency Graph nor bypass visibility, encapsulation, unidirectionality, acyclicity, or authorization constraints.

## 6. Design and Evolution Criteria

All prescriptions in this section are _recommended_ (non-binding).

- **Placement by Proximity and Domain Relevance**:
  - Place each unit according to its actual current consumers and domain significance, without positioning preemptively for nonexistent consumers.
  - **Proximity and Lowest Common Ancestor (LCA)**: Place implementation details lacking standalone domain significance at the most specific point compatible with current consumers:
    - in the matching Private Category of the single Fragment or Root Fragment whose direct-child Logical Nodes exclusively consume them (even across multiple Fragment/Root Nodes or Sub-Graph Nodes of that domain);
    - in the Fractal Branch of the lowest common ancestor Logical Domain of all consumers whenever consumers are not confined to direct-child Logical Nodes of a single Fragment or Root Fragment (e.g., across distinct subtrees, between a Fragment and a Sub-Fragment, or Category Nodes).
  - **Domain relevance and legibility by scale**: Domain legibility operates recursively at every scale rather than flattening units to the tree root: the root expresses system-wide identity, while each Functional domain reveals inside itself the primary concepts of its sub-problem. At equal scale, place a primary partition or foundational domain concept where its architectural purpose is immediately legible — as a Root Fragment at the tree root, or in the Layer/Category of the relevant Root Layer or Fractal Branch — even with a single consumer; potential technical reusability is not domain relevance.
  - **Containment matching dependency flow**: Match directory containment to dependency direction by nesting orchestrated units inside orchestrating ones rather than placing them as peer siblings with hidden dependency order; conversely, do not bury a foundational domain unit inside an auxiliary collaborator merely because the latter invokes it — coordinate both from the enclosing domain.
  - **Self-description at each scale**: At every level, a Logical Domain's direct children alone should suffice — without inspecting subtrees or code — to identify the sub-problem's units, responsibilities, and dependency flow. Concentrating primary units in a single generic auxiliary Category signals missing domain-specific Roles; procedurally named wrapper Fragments lacking standalone domain meaning and introduced only to group phases coordinated by the enclosing Functional domain should be reabsorbed into its direct-child Logical Nodes and Private Categories.
- **Depth Control — Encapsulation vs. Horizontal Hierarchy**:
  - Govern depth in priority order:
    1. **Encapsulation (default)**: first within a single Fragment via Fragment Nodes ordered by Role Ranks (when responsibilities need neither sub-domains nor dedicated Sub-Graph Nodes); then in the subtree via Private Categories and Fractal Branches so directory geometry reveals dependency flow.
    2. **Horizontal ordering** (Horizontal Hierarchies across sibling Sub-Categories, Categories, Sub-Layers, Layers, or Root Nodes): widens visibility and relies on Declarations, so use exclusively for **external exposure of dependencies** (when encapsulating in consumers' Private Categories or Fractal Branches would hide dependencies needed outside) or **semantic prominence** (surfacing core parts at the same scale without value-less intermediate domains).
  - Inside a Fractal Branch, group cohesive correlated shared responsibilities into a single Fragment (exposing contracts via `index.ts`) rather than splitting them across sibling Categories ordered by a Horizontal Hierarchy.
  - Do not place or promote a unit to a higher domain's Fractal Branch than its actual consumers warrant just to bypass Peer Separation: encapsulate a detail consumed by a single sibling Fragment in that Fragment's Private Category, or partition interdependent sibling Fragments or Category Nodes that must remain exposed into Sub-Categories ordered by a Horizontal Hierarchy.
- **Iterative and Recursive Evolution**:
  - Architecture converges iteratively over time and recursively across scale; adapt at each level via the operation with greatest conceptual economy:
    - **Extraction**: split autonomous Symbols into distinct Logical Nodes (additional Fragment Nodes, or Category Nodes in a Private Category), or turn a Fragment Node into a Sub-Fragment in a Private Category when it gains multi-Role details or needs a dedicated Sub-Graph Node (keeping it confined to the parent domain's subtree).
    - **Promotion**: upon actual consumers outside the current perimeter, move a unit into a Category (and optional Layer) of the lowest common ancestor's Fractal Branch, subject to visibility rules and Horizontal Hierarchies.
    - **Contraction**: remove or reabsorb Layers, Sub-Layers, Sub-Categories, Fractal Branches, or Sub-Fragments disproportionate to actual sub-problem complexity (including reabsorbing a Sub-Fragment into its Parent Fragment's Fragment Nodes, or collapsing a Fractal Branch or Root Layer from Layers to direct Categories).
  - Keeping a Fragment's `index.ts` contract stable makes subtree-internal refactorings transparent to external consumers.
- **External Local Dependency Isolation**:
  - During incremental adoption or alongside generated local code outside Fractal Trees, confine authorized outgoing local imports exclusively to dedicated **adapter units** (Fragments or Category Nodes in the Category and optional Layer matching the dependency's responsibility), encapsulating external modules behind a FAF-conformant contract, Role, and internal Horizontal Hierarchies to isolate future migration to a single contact point.

## 7. Static Verification (`@morriconeluca/eslint-plugin-faf`)

_Applies only when the codebase uses `@morriconeluca/eslint-plugin-faf` (`faf.config.ts`)._

- **Declarations (`faf.config.ts`)**: Authoritative Declaration source (`faf.config.ts`, or `settings.faf.configFile` in ESLint config; typed via `TFAFConfig`). Exports a synchronous `default` plain serializable object (nearest `package.json` not `"type": "commonjs"`, erasable TypeScript syntax, explicit extensions on relative value imports). Configured paths are POSIX paths relative to the config file's directory without leading `./`, `/`, trailing `/`, or `..` (`'.'` for that directory itself). Local properties replace `common` properties in full (no merging).
- **Path Aliases**: Resolved from `package.json` `"imports"` or `faf.common.aliases` (mutually exclusive — declaring both is an error); `tsconfig.json` `paths` alone is not read by the plugin.
- **Static Verification Boundaries (`faf/conformity`)**: Rejects constructs that static analysis cannot verify (`unverified/*`), including non-literal `import()` or `require()`, CommonJS `module.exports`/`exports` and `export =`, unresolved import specifiers, cyclic Root Fragment or inter-tree dependency authorizations, and symbolic links inside Fractal Trees.
- **Linting**: Verify full architectural conformity with project-wide `eslint .` without `--cache` — ESLint's `--cache` skips unchanged files on graph changes, and single-file linting omits diagnostics anchored to `faf.config.ts`, domain anchor files, or affected importers.
