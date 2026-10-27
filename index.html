
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Academic Gender Associations</title>

<style>
* { box-sizing: border-box; }

body {
  margin: 0;
  padding: 20px;
  font-family: Arial, sans-serif;
  background: #f2f5fa;
  color: #202b3c;
}

main {
  max-width: 760px;
  margin: 20px auto;
  padding: 28px;
  background: white;
  border-radius: 14px;
  box-shadow: 0 5px 24px #00000012;
}

h1 { font-size: 27px; }
.muted { color: #657187; font-size: 14px; }
.note { background: #eef3fa; padding: 15px; border-radius: 8px; }
label { display: block; margin: 15px 0; }
input, select {
  padding: 10px;
  border: 1px solid #c5cedb;
  border-radius: 6px;
  max-width: 100%;
}
button {
  padding: 12px 18px;
  margin: 8px 5px 0 0;
  background: #234e91;
  color: white;
  border: 0;
  border-radius: 7px;
  cursor: pointer;
  font-size: 15px;
}
button:disabled { opacity: .5; }
.hidden { display: none !important; }

#mapping {
  display: flex;
  gap: 12px;
  justify-content: space-between;
}
.category {
  flex: 1;
  padding: 12px;
  background: #edf2f9;
  border-radius: 7px;
  font-weight: bold;
}
#stimulus {
  min-height: 75px;
  margin: 55px 0 30px;
  text-align: center;
  font-size: clamp(28px, 6vw, 42px);
  font-weight: bold;
}
#feedback {
  min-height: 30px;
  text-align: center;
  color: #c02727;
  font-size: 25px;
  font-weight: bold;
}
#progress { margin-bottom: 15px; color: #657187; }
</style>
</head>

<body>
<main>
  <section id="intro">
    <h1>Academic Gender Associations</h1>
    <p><strong>Researcher-developed IAT-style task</strong></p>

    <div class="note">
      <p>This activity asks you to categorize words as quickly and accurately as you can.</p>
      <p>This is not the official Harvard IAT and has not been validated as a psychological measure. Participation should be voluntary and follow your school's research approval and consent procedures.</p>
      <p>Do not enter your name, email, or student number.</p>
    </div>

    <label>
      Anonymous participant code
      <br>
      <input id="participant" maxlength="30" placeholder="Use a random code">
    </label>

    <label>
      Grade
      <br>
      <select id="grade">
        <option value="">Prefer not to say</option>
        <option value="11">Grade 11</option>
        <option value="12">Grade 12</option>
      </select>
    </label>

    <label>
      <input type="checkbox" id="consent">
      I have read the information and voluntarily agree to participate.
    </label>

    <button id="start">Begin task</button>
  </section>

  <section id="task" class="hidden">
    <p id="progress"></p>

    <div id="mapping">
      <div class="category" id="left"></div>
      <div class="category" id="right" style="text-align:right"></div>
    </div>

    <div id="stimulus"></div>
    <div id="feedback" aria-live="polite"></div>

    <div class="note">
      Press <strong>E</strong> for the left category and
      <strong>I</strong> for the right category.
      If you make an error, a red X will appear. Press the
      correct key to continue.
    </div>
  </section>

  <section id="results" class="hidden">
    <h2>Task complete</h2>
    <div id="summary" class="note"></div>
    <button id="download">Download trial data (CSV)</button>
    <button id="downloadSummary">Download summary (CSV)</button>
    <button id="restart">Restart</button>
    <p class="muted">Save your downloaded files securely. Results are descriptive and should not be used to label individual participants as biased or unbiased.</p>
  </section>
</main>

<script>
(() => {
  "use strict";

  const $ = id => document.getElementById(id);

  const women = ["WOMAN", "WOMEN", "SHE", "HER", "FEMALE"];
  const men = ["MAN", "MEN", "HE", "HIM", "MALE"];

  const success = [
    "INTELLIGENT", "CAPABLE", "BRILLIANT",
    "SKILLED", "COMPETENT", "LOGICAL"
  ];

  const difficulty = [
    "STRUGGLING", "UNPREPARED", "INEPT",
    "CONFUSED", "INCAPABLE", "CARELESS"
  ];

  // Seven-block IAT-style structure.
  const blocks = [
    {type:"gender", n:20, reverse:false, practice:true},
    {type:"academic", n:20, reverse:false, practice:true},
    {type:"combined", n:20, reverse:false, practice:true},
    {type:"combined", n:40, reverse:false, practice:false},
    {type:"gender", n:20, reverse:true, practice:true},
    {type:"combined", n:20, reverse:true, practice:true},
    {type:"combined", n:40, reverse:true, practice:false}
  ];

  let blockIndex = 0;
  let trialIndex = 0;
  let blockTrials = [];
  let current = null;
  let firstKey = null;
  let firstRT = null;
  let shownAt = 0;
  let errorAt = null;
  let data = [];
  let finished = false;

  function shuffle(array) {
    const a = [...array];
    for (let i = a.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1));
      [a[i], a[j]] = [a[j], a[i]];
    }
    return a;
  }

  function poolFor(type) {
    if (type === "gender") {
      return [
        ...women.map(word => ({word, category:"Woman"})),
        ...men.map(word => ({word, category:"Man"}))
      ];
    }

    if (type === "academic") {
      return [
        ...success.map(word => ({word, category:"Academic success"})),
        ...difficulty.map(word => ({word, category:"Academic difficulty"}))
      ];
    }

    return [
      ...women.map(word => ({word, category:"Woman"})),
      ...men.map(word => ({word, category:"Man"})),
      ...success.map(word => ({word, category:"Academic success"})),
      ...difficulty.map(word => ({word, category:"Academic difficulty"}))
    ];
  }

  function makeTrials(block) {
    const pool = poolFor(block.type);
    let expanded = [];

    while (expanded.length < block.n) {
      expanded.push(...shuffle(pool));
    }

    return shuffle(expanded.slice(0, block.n));
  }

  function mapping(block) {
    if (block.type === "gender") {
      return block.reverse
        ? {left:["Man"], right:["Woman"]}
        : {left:["Woman"], right:["Man"]};
    }

    if (block.type === "academic") {
      return {
        left:["Academic success"],
        right:["Academic difficulty"]
      };
    }

    return block.reverse
      ? {
          left:["Woman", "Academic success"],
          right:["Man", "Academic difficulty"]
        }
      : {
          left:["Woman", "Academic difficulty"],
          right:["Man", "Academic success"]
        };
  }

  function start() {
    if (!$("consent").checked) {
      alert("Please confirm voluntary participation first.");
      return;
    }

    data = [];
    blockIndex = 0;
    trialIndex = 0;
    current = null;
    finished = false;

    $("intro").classList.add("hidden");
    $("results").classList.add("hidden");
    $("task").classList.remove("hidden");

    startBlock();
  }

  function startBlock() {
    if (blockIndex >= blocks.length) {
      finish();
      return;
    }

    const block = blocks[blockIndex];
    blockTrials = makeTrials(block);
    trialIndex = 0;

    const m = mapping(block);
    $("left").textContent = "E — " + m.left.join(" + ");
    $("right").textContent = "I — " + m.right.join(" + ");

    showTrial();
  }

  function showTrial() {
    if (trialIndex >= blockTrials.length) {
      blockIndex++;
      startBlock();
      return;
    }

    const block = blocks[blockIndex];
    const m = mapping(block);
    const stimulus = blockTrials[trialIndex];

    current = {
      ...stimulus,
      correctKey: m.left.includes(stimulus.category) ? "e" : "i",
      blockNumber: blockIndex + 1,
      trialNumber: trialIndex + 1,
      condition: block.reverse ? "switched" : "baseline",
      practice: block.practice
    };

    $("progress").textContent =
      `Block ${blockIndex + 1} of ${blocks.length} — ` +
      `Trial ${trialIndex + 1} of ${block.n}`;

    $("stimulus").textContent = current.word;
    $("feedback").textContent = "";

    firstKey = null;
    firstRT = null;
    errorAt = null;
    shownAt = performance.now();
  }

  function handleKey(event) {
    if ($("task").classList.contains("hidden") ||
        finished || !current) return;

    const key = event.key.toLowerCase();
    if (key !== "e" && key !== "i") return;

    event.preventDefault();

    const now = performance.now();

    if (firstKey === null) {
      firstKey = key;
      firstRT = Math.round(now - shownAt);

      if (key === current.correctKey) {
        saveTrial(true, now, null);
      } else {
        errorAt = now;
        $("feedback").textContent = "✕";
      }
      return;
    }

    if (key === current.correctKey) {
      saveTrial(false, now, Math.round(now - errorAt));
    }
  }

  function saveTrial(correctFirst, now, correctionRT) {
    data.push({
      participant_code: $("participant").value.trim() || "not_provided",
      grade: $("grade").value || "not_provided",
      timestamp_utc: new Date().toISOString(),
      block_number: current.blockNumber,
      trial_number: current.trialNumber,
      condition: current.condition,
      practice_block: current.practice,
      stimulus: current.word,
      category: current.category,
      correct_key: current.correctKey.toUpperCase(),
      first_response_key: firstKey.toUpperCase(),
      first_response_correct: correctFirst,
      first_response_rt_ms: firstRT,
      error_correction_rt_ms: correctionRT,
      total_rt_to_correct_ms: Math.round(now - shownAt)
    });

    current = null;
    trialIndex++;
    setTimeout(showTrial, 180);
  }

  function mean(values) {
    return values.length
      ? values.reduce((sum, value) => sum + value, 0) / values.length
      : null;
  }

  function finish() {
    finished = true;
    $("task").classList.add("hidden");
    $("results").classList.remove("hidden");

    const tests = data.filter(t => !t.practice_block);
    const baseline = tests
      .filter(t => t.condition === "baseline")
      .map(t => t.total_rt_to_correct_ms);

    const switched = tests
      .filter(t => t.condition === "switched")
      .map(t => t.total_rt_to_correct_ms);

    const responses = data.filter(t => t.first_response_rt_ms !== null);
    const errors = responses.filter(t => !t.first_response_correct).length;
    const accuracy = responses.length
      ? 100 * (responses.length - errors) / responses.length
      : 0;

    const baseMean = mean(baseline);
    const switchMean = mean(switched);

    $("summary").innerHTML = `
      <p>Trials recorded: ${data.length}</p>
      <p>First-response accuracy: ${accuracy.toFixed(1)}%</p>
      <p>First-response errors: ${errors}</p>
      <p>Baseline mean time: ${baseMean === null ? "N/A" : Math.round(baseMean) + " ms"}</p>
      <p>Switched mean time: ${switchMean === null ? "N/A" : Math.round(switchMean) + " ms"}</p>
      <p>Descriptive difference (switched − baseline):
      ${baseMean === null || switchMean === null
        ? "N/A"
        : Math.round(switchMean - baseMean) + " ms"}</p>
      <p class="muted">This is not a validated IAT D-score.</p>
    `;
  }

  function csvEscape(value) {
    if (value === null || value === undefined) return "";
    const s = String(value);
    return /[",\n\r]/.test(s)
      ? '"' + s.replace(/"/g, '""') + '"'
      : s;
  }

  function downloadCSV(filename, rows) {
    if (!rows.length) {
      alert("There is no data to download.");
      return;
    }

    const keys = [...new Set(rows.flatMap(row => Object.keys(row)))];
    const content = [
      keys.map(csvEscape).join(","),
      ...rows.map(row => keys.map(key => csvEscape(row[key])).join(","))
    ].join("\r\n");

    const blob = new Blob(["\ufeff" + content], {
      type: "text/csv;charset=utf-8"
    });

    const url = URL.createObjectURL(blob);
    const link = document.createElement("a");
    link.href = url;
    link.download = filename;
    link.click();
    setTimeout(() => URL.revokeObjectURL(url), 1000);
  }

  $("start").addEventListener("click", start);

  $("download").addEventListener("click", () => {
    downloadCSV("academic_gender_iat_trials.csv", data);
  });

  $("downloadSummary").addEventListener("click", () => {
    const tests = data.filter(t => !t.practice_block);
    const base = tests.filter(t => t.condition === "baseline")
      .map(t => t.total_rt_to_correct_ms);
    const switched = tests.filter(t => t.condition === "switched")
      .map(t => t.total_rt_to_correct_ms);
    const responses = data.filter(t => t.first_response_rt_ms !== null);
    const errors = responses.filter(t => !t.first_response_correct).length;
    const avg = values => mean(values) === null
      ? ""
      : Math.round(mean(values));

    downloadCSV("academic_gender_iat_summary.csv", [{
      participant_code: $("participant").value.trim() || "not_provided",
      grade: $("grade").value || "not_provided",
      timestamp_utc: new Date().toISOString(),
      trials_recorded: data.length,
      first_response_accuracy_percent: responses.length
        ? ((responses.length - errors) / responses.length * 100).toFixed(1)
        : "",
      first_response_errors: errors,
      baseline_mean_rt_ms: avg(base),
      switched_mean_rt_ms: avg(switched),
      switched_minus_baseline_ms:
        base.length && switched.length ? avg(switched) - avg(base) : "",
      note: "Researcher-developed, unvalidated IAT-style task"
    }]);
  });

  $("restart").addEventListener("click", () => {
    if (confirm("Restart and discard the current in-memory data? Download it first if needed.")) {
      data = [];
      current = null;
      finished = false;
      $("results").classList.add("hidden");
      $("task").classList.add("hidden");
      $("intro").classList.remove("hidden");
    }
  });

  document.addEventListener("keydown", handleKey);
})();
</script>
</body>
</html>
