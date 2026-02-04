<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
</head>

<body>

<h1 class="center">LISA – Lightweight Instruction Set Architecture Processor</h1>

<p>
<b>LISA (Lightweight Instruction Set Architecture)</b> is a custom-designed
<b>16-bit multi-cycle processor architecture</b> built completely from scratch at the
hardware-logic and control-signal level. It implements a full computing stack —
from instruction set design to compiler — to model how real processors operate internally.
</p>

<p>
Unlike emulators or high-level simulators, every component is explicitly designed
at the register-transfer level, closely resembling how real CPUs are implemented.
</p>

<hr>

<h2>✨ Features</h2>

<ul>
<li>Custom ISA design</li>
<li>Hardwired Control Unit (no microcode)</li>
<li>Multi-cycle datapath</li>
<li>Address Generation Unit (AGU)</li>
<li>Stack-based execution model</li>
<li>Memory-mapped I/O</li>
<li>Custom assembler</li>
<li>Custom C++-like compiler</li>
<li>End-to-end toolchain</li>
</ul>

<hr>

<h2>🧠 Architecture Overview</h2>

<p>LISA follows a multi-cycle CPU design where each instruction is executed across multiple phases:</p>

<pre>Fetch → Decode → Operand Read → Execute → Writeback → Commit</pre>

<ul>
<li>Simplifies hardware</li>
<li>Reduces combinational complexity</li>
<li>Improves scalability</li>
<li>Mirrors educational CPUs like MIPS multi-cycle designs</li>
</ul>

<hr>

<h2>⚙️ Core Components</h2>

<h3>1️⃣ Control Unit (CU)</h3>

<ul>
<li>6-bit opcode</li>
<li>6 → 64 one-hot decoder</li>
<li>Hardwired control signals</li>
<li>No microcode</li>
<li>Dual ring counters for timing</li>
</ul>

<hr>

<h3>2️⃣ Instruction Fetch Unit</h3>

<p><b>Instruction width:</b> 64 bits<br>
<b>ROM width:</b> 32 bits</p>

<p>Each instruction is fetched in two cycles:</p>

<ol>
<li>Address ROM</li>
<li>Load upper 32 bits</li>
<li>Increment pointer</li>
<li>Load lower 32 bits</li>
</ol>

<hr>

<h3>3️⃣ Instruction Format</h3>

<table>
<tr>
<th>Field</th>
<th>Bits</th>
<th>Description</th>
</tr>
<tr>
<td>Opcode</td>
<td>6</td>
<td>Instruction selection</td>
</tr>
<tr>
<td>addr1, addr2, addr3</td>
<td>16 each</td>
<td>Operand offsets</td>
</tr>
<tr>
<td>Mode</td>
<td>6</td>
<td>Base addressing mode</td>
</tr>
<tr>
<td>Size</td>
<td>2</td>
<td>Data width control</td>
</tr>
<tr>
<td>Spare</td>
<td>2</td>
<td>Reserved</td>
</tr>
</table>

<hr>

<h3>4️⃣ Datapath</h3>

<ul>
<li>Shared memory bus</li>
<li>Operand registers</li>
<li>ALU</li>
<li>Stack pointer unit</li>
<li>AGU</li>
<li>Instruction Register (64-bit)</li>
</ul>

<hr>

<h3>5️⃣ Address Generation Unit (AGU)</h3>

<pre>effective_address = base + offset</pre>

<ul>
<li>BP → Stack</li>
<li>HP → Heap</li>
<li>GN → Global</li>
<li>Supports stack-relative, heap-relative, register-indirect modes</li>
<li>Programs become relocatable</li>
</ul>

<hr>

<h3>6️⃣ Stack Pointer Unit</h3>

<ul>
<li>Push / Pop</li>
<li>Increment / Decrement</li>
<li>Direct assignment</li>
<li>Pre-update and post-update semantics</li>
</ul>

<hr>

<h3>7️⃣ ALU</h3>

<ul>
<li>Arithmetic</li>
<li>Logic</li>
<li>Comparisons</li>
<li>Data movement</li>
<li>Dynamic width based on instruction size field</li>
</ul>

<hr>

<h3>8️⃣ Memory-Mapped I/O</h3>

<ul>
<li>ASCII character display (console output)</li>
<li>GPIO digital pins</li>
<li>No special I/O instructions required</li>
</ul>

<hr>

<h2>🛠 Toolchain</h2>

<pre>
Source Code → Compiler → Assembly → Assembler → Machine Code → ROM → LISA CPU
</pre>

<ul>
<li>Assembler → converts assembly to machine code</li>
<li>C++-like compiler → high-level language support</li>
</ul>

<hr>

<h2>📚 Learning Goals</h2>

<ul>
<li>CPU microarchitecture</li>
<li>Control logic design</li>
<li>Instruction set design</li>
<li>Memory systems</li>
<li>Stack machines</li>
<li>Compiler backend basics</li>
</ul>

<hr>

<h2>🎯 Why This Project Matters</h2>

<p>This is not just a simulator. It demonstrates:</p>

<ul>
<li>Cycle-level execution</li>
<li>Bus arbitration</li>
<li>Control signal design</li>
<li>Real hardware thinking</li>
<li>Full hardware–software integration</li>
</ul>

<hr>

<h2>🚧 Future Improvements</h2>

<ul>
<li>Pipelining</li>
<li>Interrupts</li>
<li>Caching</li>
<li>Virtual memory</li>
<li>Branch prediction</li>
<li>Multitasking</li>
<li>FPGA implementation</li>
</ul>

<hr>

<h2>📌 Project Status</h2>

<ul>
<li>✅ Architecture finalized</li>
<li>✅ Control unit complete</li>
<li>✅ Datapath working</li>
<li>✅ Compiler + assembler functional</li>
<li>✅ End-to-end programs running</li>
</ul>

<hr>

<h2 class="center">Images</h2>

<p class="center">
<img src="https://github.com/JADUxy/custom_isa_logisim_proccessor/blob/main/Screenshot%202026-02-03%20224117.png" width="500" alt="Architecture Image">
</p>


## 🎬 Demo Video

[![Watch Demo](https://raw.githubusercontent.com/JADUxy/custom_isa_logisim_proccessor/refs/heads/main/Screenshot%202026-02-03%20222448.png)](https://www.reddit.com/r/logisim/comments/1quze08/finished_working_32_bit_proccessor/)


</body>
</html>
