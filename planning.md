# TakeMeter Planning Document

## Project Title

One Piece TakeMeter: Classifying Discussion Styles in One Piece Communities

## Community

This project focuses on One Piece discussion communities on Reddit. The primary sources of data will be:

- r/OnePiece
- r/shounenfolk
- r/OnePiecePowerScaling

These communities contain a wide variety of discussion styles ranging from detailed story analysis to emotional reactions and personal opinions. This makes them well-suited for a discourse classification task.

## Classification Task

The goal of this project is to classify comments into one of three discussion styles:

1. Analysis
2. Opinion
3. Reaction

## Label Definitions

### Analysis

Comments that support their claims using evidence, examples, reasoning, comparisons, or detailed explanations.

Characteristics:

- References specific story events
- Explains why something happened
- Uses evidence to support a conclusion
- Compares characters, arcs, themes, or powers

Examples:

- Explaining Robin's development in Enies Lobby
- Discussing why Wano's storytelling succeeded or failed
- Comparing the strength of different characters using evidence

### Opinion

Comments that express a personal preference, judgment, or ranking without substantial supporting analysis.

Characteristics:

- States likes or dislikes
- Ranks characters or arcs
- Makes subjective judgments
- Limited reasoning

Examples:

- "Fishman Island is the worst arc."
- "Dressrosa is overrated."
- "Zoro is my favorite Straw Hat."

### Reaction

Comments that primarily express an emotional response to an episode, chapter, reveal, scene, character, or event.

Characteristics:

- Excitement
- Surprise
- Frustration
- Humor
- Shock

Examples:

- "That episode was amazing!"
- "I can't believe Oda did that."
- "Shamrock's voice actor is perfect."

## Edge Cases

### Analysis vs Opinion

Many comments contain opinions and analysis together.

Decision Rule:
If a comment provides substantial evidence, examples, or reasoning to support a claim, it will be labeled Analysis.

Example:

"Wano failed because Kaido lacked personal stakes, there were too many characters, and the raid had pacing issues."

Label: Analysis

Example:

"Wano is overrated."

Label: Opinion

### Opinion vs Reaction

Some comments express both a judgment and an emotional response.

Decision Rule:
If the main purpose is expressing emotion, label as Reaction.

Example:

"That reveal was insane!"

Label: Reaction

Example:

"That reveal was poorly written."

Label: Opinion

## Data Collection Plan

Data will be collected manually from Reddit discussions related to One Piece.

Sources:

- Character development discussions
- Arc rankings and reviews
- Episode discussion threads
- Chapter discussion threads
- Power scaling discussions
- Community hot takes

Target dataset size:

- Analysis: ~70 examples
- Opinion: ~70 examples
- Reaction: ~70 examples

Total target:

- Approximately 210 labeled examples

Dataset format:

text,label

## Baseline Evaluation

A zero-shot baseline will be created using a large language model through Groq.

Metrics:

- Accuracy
- Precision
- Recall
- F1 Score

The baseline results will be compared against the fine-tuned DistilBERT classifier.

## Fine-Tuning Plan

Model:

- DistilBERT

Training:

- Use the provided Colab notebook
- Split dataset into training and evaluation sets
- Fine-tune using labeled examples

## Success Criteria

The project will be considered successful if:

- The fine-tuned model outperforms the zero-shot baseline in accuracy and F1 score.
- Labels remain consistent across the dataset
- The model correctly distinguishes between Analysis, Opinion, and Reaction comments
- The confusion matrix shows reasonable separation between classes

## Expected Challenges

- Distinguishing Analysis from Opinion
- Handling very short comments
- Handling comments that contain multiple discussion styles

## Evaluation Metrics

The primary evaluation metrics will be:

- Accuracy
- Precision
- Recall
- F1 Score
- Confusion Matrix

Accuracy alone is not sufficient because a model can achieve a high accuracy score while still performing poorly on one specific label. Precision and recall help measure how well the model identifies each class individually, while the F1 score balances both metrics. The confusion matrix will be used to identify which labels are most commonly confused with one another, particularly Analysis and Opinion.

## Definition of Success

The classifier will be considered successful if:

- Overall accuracy is at least 80%.
- Each label achieves an F1 score of at least 0.75.
- The fine-tuned DistilBERT model outperforms the zero-shot baseline.
- The confusion matrix shows that Analysis, Opinion, and Reaction are generally separated correctly.

These thresholds would make the classifier useful as a moderation or community analytics tool for identifying discussion styles in One Piece communities.

## Dataset Balance Strategy

Target dataset size:

- Analysis: ~70 examples
- Opinion: ~70 examples
- Reaction: ~70 examples

If one label is underrepresented after collecting approximately 200 examples, additional examples will be gathered specifically from discussion sources that naturally contain that label.

For example:

- Analysis: Character analysis and arc discussion threads
- Opinion: Arc ranking and hot take threads
- Reaction: Chapter discussion and episode reaction threads

## Label Examples

### Analysis

Example 1:
"Luffy learned the consequences of his actions after Sabaody and Marineford."

Example 2:
"Fishman Island demonstrates the cycle of hatred through Hody Jones."

### Opinion

Example 1:
"Fishman Island is the worst arc."

Example 2:
"Zoro is the best Straw Hat."

### Reaction

Example 1:
"That chapter blew my mind."

Example 2:
"I can't wait for next week's episode."

## AI Tool Plan

### Label Stress-Testing

AI tools will be used to generate ambiguous examples that fall between Analysis, Opinion, and Reaction. If generated examples cannot be classified consistently, label definitions will be refined before training.

### Annotation Assistance

AI tools may be used to suggest potential labels during dataset collection, but all labels included in the final dataset will be manually reviewed and assigned by the project author.

### Failure Analysis

After model evaluation, incorrect predictions will be provided to an AI tool to identify possible patterns of failure. Any suggested patterns will be verified manually by reviewing the original examples and confusion matrix results.
