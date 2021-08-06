---
keywords: fastai
description: "altair 画图测试"
title: "南京疫情数据"
badges: false
author: 王一刀
categories: [南京疫情]
nb_path: _notebooks/2021-07-30-ipynb-test.ipynb
layout: notebook
---

<!--
#################################################
### THIS FILE WAS AUTOGENERATED! DO NOT EDIT! ###
#################################################
# file to edit: _notebooks/2021-07-30-ipynb-test.ipynb
-->

<div class="container" id="notebook-container">
        
    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="kn">import</span> <span class="nn">pandas</span> <span class="k">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">altair</span> <span class="k">as</span> <span class="nn">alt</span>

<span class="n">cols</span> <span class="o">=</span> <span class="p">[</span><span class="s2">&quot;日期&quot;</span><span class="p">,</span><span class="s2">&quot;重症&quot;</span><span class="p">,</span><span class="s2">&quot;普通&quot;</span><span class="p">,</span><span class="s2">&quot;轻型&quot;</span><span class="p">,</span><span class="s2">&quot;无症状&quot;</span><span class="p">,</span><span class="s2">&quot;重症累计&quot;</span><span class="p">,</span><span class="s2">&quot;普通累计&quot;</span><span class="p">,</span><span class="s2">&quot;轻型累计&quot;</span><span class="p">,</span><span class="s2">&quot;无症状累计&quot;</span><span class="p">]</span>

<span class="n">data</span> <span class="o">=</span> <span class="p">[</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-21&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">8</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">8</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-22&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">7</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">12</span><span class="p">,</span><span class="mi">11</span><span class="p">,</span><span class="mi">14</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-23&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">9</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">4</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">21</span><span class="p">,</span><span class="mi">14</span><span class="p">,</span><span class="mi">18</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-24&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">23</span><span class="p">,</span><span class="mi">14</span><span class="p">,</span><span class="mi">20</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-25&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">11</span><span class="p">,</span><span class="mi">27</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">32</span><span class="p">,</span><span class="mi">41</span><span class="p">,</span><span class="mi">13</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-26&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">28</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">38</span><span class="p">,</span><span class="mi">66</span><span class="p">,</span><span class="mi">6</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-27&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">24</span><span class="p">,</span><span class="mi">23</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">4</span><span class="p">,</span><span class="mi">68</span><span class="p">,</span><span class="mi">81</span><span class="p">,</span><span class="mi">2</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-28&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">8</span><span class="p">,</span><span class="mi">10</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">7</span><span class="p">,</span><span class="mi">86</span><span class="p">,</span><span class="mi">78</span><span class="p">,</span><span class="mi">2</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-29&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">10</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">8</span><span class="p">,</span><span class="mi">94</span><span class="p">,</span><span class="mi">82</span><span class="p">,</span><span class="mi">1</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-30&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">8</span><span class="p">,</span><span class="mi">95</span><span class="p">,</span><span class="mi">87</span><span class="p">,</span><span class="mi">1</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-07-31&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">12</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">7</span><span class="p">,</span><span class="mi">114</span><span class="p">,</span><span class="mi">83</span><span class="p">,</span><span class="mi">0</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-08-01&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">5</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">7</span><span class="p">,</span><span class="mi">127</span><span class="p">,</span><span class="mi">81</span><span class="p">,</span><span class="mi">0</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-08-02&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">3</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">6</span><span class="p">,</span><span class="mi">132</span><span class="p">,</span><span class="mi">82</span><span class="p">,</span><span class="mi">0</span><span class="p">],</span>
    <span class="p">[</span><span class="s1">&#39;2021-08-03&#39;</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">1</span><span class="p">,</span><span class="mi">0</span><span class="p">,</span><span class="mi">2</span><span class="p">,</span><span class="mi">143</span><span class="p">,</span><span class="mi">78</span><span class="p">,</span><span class="mi">0</span><span class="p">]</span>
<span class="p">]</span>

<span class="n">alldf</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span><span class="p">(</span><span class="n">data</span><span class="o">=</span><span class="n">data</span><span class="p">,</span><span class="n">columns</span><span class="o">=</span><span class="n">cols</span><span class="p">)</span>

<span class="n">df1</span> <span class="o">=</span> <span class="n">alldf</span><span class="o">.</span><span class="n">melt</span><span class="p">(</span><span class="n">id_vars</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;日期&quot;</span><span class="p">],</span><span class="n">value_vars</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;重症&quot;</span><span class="p">,</span><span class="s2">&quot;普通&quot;</span><span class="p">,</span><span class="s2">&quot;轻型&quot;</span><span class="p">,</span><span class="s2">&quot;无症状&quot;</span><span class="p">],</span><span class="n">var_name</span><span class="o">=</span><span class="s2">&quot;症状&quot;</span><span class="p">,</span><span class="n">value_name</span><span class="o">=</span><span class="s2">&quot;人数&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;日期&quot;</span><span class="p">])</span>

<span class="n">alt</span><span class="o">.</span><span class="n">Chart</span><span class="p">(</span><span class="n">df1</span><span class="p">)</span><span class="o">.</span><span class="n">mark_line</span><span class="p">()</span><span class="o">.</span><span class="n">encode</span><span class="p">(</span>
    <span class="n">x</span><span class="o">=</span><span class="s1">&#39;日期&#39;</span><span class="p">,</span>
    <span class="n">y</span><span class="o">=</span><span class="s1">&#39;人数&#39;</span><span class="p">,</span>
    <span class="n">color</span><span class="o">=</span><span class="s1">&#39;症状&#39;</span><span class="p">,</span>
    <span class="n">strokeDash</span><span class="o">=</span><span class="s1">&#39;症状&#39;</span><span class="p">,</span>
<span class="p">)</span><span class="o">.</span><span class="n">properties</span><span class="p">(</span>
    <span class="n">title</span><span class="o">=</span><span class="s1">&#39;南京疫情 每日新增&#39;</span><span class="p">,</span>
    <span class="n">width</span><span class="o">=</span><span class="mi">700</span><span class="p">,</span>
    <span class="n">height</span><span class="o">=</span><span class="mi">450</span>
<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">


<div class="output_html rendered_html output_subarea output_execute_result">

<div id="altair-viz-7a5c8a9754114ec598a14828ef24ed96"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-7a5c8a9754114ec598a14828ef24ed96") {
      outputDiv = document.getElementById("altair-viz-7a5c8a9754114ec598a14828ef24ed96");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "data": {"name": "data-851cecfc6d7fd451abc9342b13f6e60f"}, "mark": "line", "encoding": {"color": {"type": "nominal", "field": "\u75c7\u72b6"}, "strokeDash": {"type": "nominal", "field": "\u75c7\u72b6"}, "x": {"type": "nominal", "field": "\u65e5\u671f"}, "y": {"type": "quantitative", "field": "\u4eba\u6570"}}, "height": 450, "title": "\u5357\u4eac\u75ab\u60c5 \u6bcf\u65e5\u65b0\u589e", "width": 700, "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-851cecfc6d7fd451abc9342b13f6e60f": [{"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 5}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 8}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 5}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 7}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 3}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 4}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 9}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 27}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 11}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 3}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 28}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 24}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 23}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 10}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 8}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 10}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 3}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 5}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 12}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 5}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 3}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u666e\u901a", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u91cd\u75c7", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u8f7b\u578b", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u65e0\u75c7\u72b6", "\u4eba\u6570": 0}]}}, {"mode": "vega-lite"});
</script>
</div>

</div>

</div>
</div>

</div>
    {% endraw %}

    {% raw %}
    
<div class="cell border-box-sizing code_cell rendered">
<div class="input">

<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython3"><pre><span></span><span class="n">df2</span> <span class="o">=</span> <span class="n">alldf</span><span class="o">.</span><span class="n">melt</span><span class="p">(</span><span class="n">id_vars</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;日期&quot;</span><span class="p">],</span><span class="n">value_vars</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;重症累计&quot;</span><span class="p">,</span><span class="s2">&quot;普通累计&quot;</span><span class="p">,</span><span class="s2">&quot;轻型累计&quot;</span><span class="p">,</span><span class="s2">&quot;无症状累计&quot;</span><span class="p">],</span><span class="n">var_name</span><span class="o">=</span><span class="s2">&quot;症状&quot;</span><span class="p">,</span><span class="n">value_name</span><span class="o">=</span><span class="s2">&quot;人数&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">sort_values</span><span class="p">(</span><span class="n">by</span><span class="o">=</span><span class="p">[</span><span class="s2">&quot;日期&quot;</span><span class="p">])</span>

<span class="n">alt</span><span class="o">.</span><span class="n">Chart</span><span class="p">(</span><span class="n">df2</span><span class="p">)</span><span class="o">.</span><span class="n">mark_line</span><span class="p">()</span><span class="o">.</span><span class="n">encode</span><span class="p">(</span>
    <span class="n">x</span><span class="o">=</span><span class="s1">&#39;日期&#39;</span><span class="p">,</span>
    <span class="n">y</span><span class="o">=</span><span class="s1">&#39;人数&#39;</span><span class="p">,</span>
    <span class="n">color</span><span class="o">=</span><span class="s1">&#39;症状&#39;</span><span class="p">,</span>
    <span class="n">strokeDash</span><span class="o">=</span><span class="s1">&#39;症状&#39;</span><span class="p">,</span>
<span class="p">)</span><span class="o">.</span><span class="n">properties</span><span class="p">(</span>
    <span class="n">title</span><span class="o">=</span><span class="s1">&#39;南京疫情 每日累计&#39;</span><span class="p">,</span>
    <span class="n">width</span><span class="o">=</span><span class="mi">700</span><span class="p">,</span>
    <span class="n">height</span><span class="o">=</span><span class="mi">450</span>
<span class="p">)</span>
</pre></div>

    </div>
</div>
</div>

<div class="output_wrapper">
<div class="output">

<div class="output_area">


<div class="output_html rendered_html output_subarea output_execute_result">

<div id="altair-viz-6e2911a5555147c6991dbb4c42b3d9d3"></div>
<script type="text/javascript">
  (function(spec, embedOpt){
    let outputDiv = document.currentScript.previousElementSibling;
    if (outputDiv.id !== "altair-viz-6e2911a5555147c6991dbb4c42b3d9d3") {
      outputDiv = document.getElementById("altair-viz-6e2911a5555147c6991dbb4c42b3d9d3");
    }
    const paths = {
      "vega": "https://cdn.jsdelivr.net/npm//vega@5?noext",
      "vega-lib": "https://cdn.jsdelivr.net/npm//vega-lib?noext",
      "vega-lite": "https://cdn.jsdelivr.net/npm//vega-lite@4.8.1?noext",
      "vega-embed": "https://cdn.jsdelivr.net/npm//vega-embed@6?noext",
    };

    function loadScript(lib) {
      return new Promise(function(resolve, reject) {
        var s = document.createElement('script');
        s.src = paths[lib];
        s.async = true;
        s.onload = () => resolve(paths[lib]);
        s.onerror = () => reject(`Error loading script: ${paths[lib]}`);
        document.getElementsByTagName("head")[0].appendChild(s);
      });
    }

    function showError(err) {
      outputDiv.innerHTML = `<div class="error" style="color:red;">${err}</div>`;
      throw err;
    }

    function displayChart(vegaEmbed) {
      vegaEmbed(outputDiv, spec, embedOpt)
        .catch(err => showError(`Javascript Error: ${err.message}<br>This usually means there's a typo in your chart specification. See the javascript console for the full traceback.`));
    }

    if(typeof define === "function" && define.amd) {
      requirejs.config({paths});
      require(["vega-embed"], displayChart, err => showError(`Error loading script: ${err.message}`));
    } else if (typeof vegaEmbed === "function") {
      displayChart(vegaEmbed);
    } else {
      loadScript("vega")
        .then(() => loadScript("vega-lite"))
        .then(() => loadScript("vega-embed"))
        .catch(showError)
        .then(() => displayChart(vegaEmbed));
    }
  })({"config": {"view": {"continuousWidth": 400, "continuousHeight": 300}}, "data": {"name": "data-ccf4605fcf19e8906a73e08e58ae4e26"}, "mark": "line", "encoding": {"color": {"type": "nominal", "field": "\u75c7\u72b6"}, "strokeDash": {"type": "nominal", "field": "\u75c7\u72b6"}, "x": {"type": "nominal", "field": "\u65e5\u671f"}, "y": {"type": "quantitative", "field": "\u4eba\u6570"}}, "height": 450, "title": "\u5357\u4eac\u75ab\u60c5 \u6bcf\u65e5\u7d2f\u8ba1", "width": 700, "$schema": "https://vega.github.io/schema/vega-lite/v4.8.1.json", "datasets": {"data-ccf4605fcf19e8906a73e08e58ae4e26": [{"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 5}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 8}, {"\u65e5\u671f": "2021-07-21", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 11}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 12}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 14}, {"\u65e5\u671f": "2021-07-22", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 14}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 18}, {"\u65e5\u671f": "2021-07-23", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 21}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 14}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 23}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 20}, {"\u65e5\u671f": "2021-07-24", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 41}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 32}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 13}, {"\u65e5\u671f": "2021-07-25", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 38}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 66}, {"\u65e5\u671f": "2021-07-26", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 68}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 81}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-27", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 4}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 78}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 86}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-07-28", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 7}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 82}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 94}, {"\u65e5\u671f": "2021-07-29", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 8}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 87}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 1}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 95}, {"\u65e5\u671f": "2021-07-30", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 8}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 83}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 114}, {"\u65e5\u671f": "2021-07-31", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 7}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 81}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 7}, {"\u65e5\u671f": "2021-08-01", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 127}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 82}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 132}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 6}, {"\u65e5\u671f": "2021-08-02", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 0}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u666e\u901a\u7d2f\u8ba1", "\u4eba\u6570": 143}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u91cd\u75c7\u7d2f\u8ba1", "\u4eba\u6570": 2}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u8f7b\u578b\u7d2f\u8ba1", "\u4eba\u6570": 78}, {"\u65e5\u671f": "2021-08-03", "\u75c7\u72b6": "\u65e0\u75c7\u72b6\u7d2f\u8ba1", "\u4eba\u6570": 0}]}}, {"mode": "vega-lite"});
</script>
</div>

</div>

</div>
</div>

</div>
    {% endraw %}

</div>
 
