---
layout: post
title: 问题调研
---

问题调研的目的是：掌握一个问题最新的研究进展，思考自己如何在这个问题上开展工作。

## 选择研究问题

我们的研究一般来说分为以下方向：

Option A (Literature survey):
- Pick a problem that interests you
- Search the literature for AI approaches to tackle this problem
- Survey and discuss the relative strengths of each approach
- If you'd like to see examples of survey papers in AI, have a look at the IJCAI-2021 survey track

Option B (Empirical evaluation):
- Pick a problem that interests you.
- Implement and experiment with several machine learning techniques to tackle this problem.

Option C (Algorithm design):
- Identify a problem for which there are no satisfying approaches.
- Develop an AI technique to tackle this problem.
- Analyze theoretically and/or empirically the performance of your technique.

Option D (Dataset/Simulator/Benchmark design):
- Identify a problem for which there is a lack of datasets or benchmarks to evaluate AI algorithms.
- Collect a dataset or design a new benchmark to evaluate AI algorithms.
- Demonstrate how some baseline AI algorithms perform with your dataset or benchmark.
- If you'd like to see examples of papers describing datasets or benchmarks, have a look at the NeurIPS-2021 datasets and benchmarks track

Option E (Theoretical analysis):
- Identify a problem or machine learning technique for which the properties (e.g., complexity, performance) are not well understood.
- Analyze the properties of this problem or technique.

## 制定调研计划

选择一个你喜欢的研究方向后，我们首先制定研究计划。

请提交研究计划，规则如下：

- Submit electronically on the LEARN website by June 30 (11:59 pm)
- At most one page (excluding references)
- Use the JMLR format: https://www.jmlr.org/format/format.html

研究计划中包括的内容：

Which option did you pick?

Option A (Literature survey):
- What is the problem?
- Cite 8 to 12 papers that you plan to survey.

Option B (Empirical evaluation):
- What is the problem?
- What AI techniques do you plan to experiment with?
- Cite 4 to 8 related papers that you plan to review.

Option C (Algorithm design):
- What is the problem?
- Why are there no satisfying approaches?
- What is the intuition behind the new technique that you plan to develop?
- Cite 4 to 8 related papers that you plan to review.

Option D (Dataset/Simulator/Benchmark design):
- What is the AI problem for which there is a lack of datasets or benchmarks?
- What dataset or benchmark do you plan to design?
- Cite 4 to 8 related papers that you plan to review.

Option E (Theoretical analysis):
- What is the problem or technique that you plan to analyze?
- What properties would you like to analyze/prove about this problem or technique?
- Cite 4 to 8 related papers that you plan to review.

## 调研报告

进行调研，提交调研报告。

报告要求如下：
- At most 8 pages (excluding references)
- Use the JMLR format: https://www.jmlr.org/format/format.html
- Explain the big picture and any necessary detail
- Submit electronically on the LEARN website by August 16 (11:59 pm)

Suggested Structure for the Report：

Option A (Literature survey):
- Introduction
  - What is the problem?
  - Why is it an important problem?
- Survey
  - Summarize the range of techniques by highlighting their strengths and weaknesses (i.e., the 8-12 papers that you read)
  - Tip: this summary should not be a laundry list of techniques with an independent paragraph for each technique
  - Suggestion: organize your summary based on desirable properties of the techniques
- Analysis:
  - What is the state of the art?
- Any open problem?
- Conclusion
  - What have you learned?
  - What future research do you recommend?

Option B (Empirical evaluation):
- Introduction
  - What is the problem?
  - Why is it an important problem?
- Techniques to tackle the problem
  - Brief review of previous work concerning this problem (i.e., the 4-8 papers that you read)
  - Brief description of the techniques chosen and why
- Empirical evaluation
  - Compare empirically the techniques for complexity, performance, ease of use, etc.
- Conclusion:
  - What is the best technique?
  - Is any technique good enough to declare the problem solved?
  - What future research do you recommend?

Option C (Algorithm design):
- Introduction
  - What is the problem?
  - Why can't any of the existing techniques effectively tackle this problem?
  - What is the intuition behind the technique that you have developed?
- Techniques to tackle the problem
  - Brief review of previous work concerning this problem (i.e., the 4-8 papers that you read)
  - Describe the technique that you developed
  - Brief description of the existing techniques that you will compare to
- Evaluation
  - Analyze and compare (empirically or theoretically) your new approach to existing approaches
- Conclusion:
  - Can your new technique effectively tackle the problem?
  - What future research do you recommend?

Option D (Dataset/Benchmark):
- Introduction
  - What is the problem?
  - Why aren't existing datasets or benchmarks sufficient to evaluate techniques for this problem?
- Proposed Dataset or Benchmark
  - Describe the proposed dataset or benchmnark
  - Describe the properties of the dataset or benchmark that are unique
- Evaluation
  - Brief description of some baseline techniques that you plan to evaluate
  - Compare empirically the baseline techniques with your dataset or benchmark
- Conclusion:
  - What are the most important weaknesses of existing baselines that your dataset or benchmark highlighted
  - What future research do you recommend?

Option E (Theoretical analysis):
- Introduction
  - What is the problem or technique?
  - What properties did you analyze/prove about this problem or technique?
- Analysis
  - Brief survey of previous work concerning this problem (i.e., the 4-8 papers that you read)
  - Describe the analysis performed
- Conclusion:
  - What have you discovered about the technique analyzed?
  - What future research do you recommend?

## 参考

- 滑铁卢大学 CS486 问题调研说明，[Webpage](https://cs.uwaterloo.ca/~ppoupart/teaching/cs486-spring23/project.html)

<br/>

|[Index](./) | [Previous](5-3-critical) | [Next](50-project)
