# Machine-Project-Expert-System-for-Diagnosing-Dental-Conditions
This expert system is designed to assist in diagnosing various dental conditions based on symptoms and observations. It uses a knowledge base of rules and certainty factors to infer diagnoses.

## How to Use

1. **Initialization and Execution**
    - To start the expert system, use the query:
        ```prolog
        solve(diagnose(X), CF).
        ```
        - `X` will be the diagnosis, and `CF` will be the certainty factor of the diagnosis.

2. **User Interaction**
    - The system will ask a series of queries about symptoms and observations. Your responses must be one of the following:
        - A number between -100 and 100 representing your confidence in the truth of the query.
        - `why` to get an explanation of the current query.
        - `how(X)` to understand how a particular goal `X` was concluded.
    - For each query, respond with an appropriate answer based on the observed symptoms or examination results.

3. **Thresholds and Certainty Factors**
    - The system uses certainty factors to measure confidence in the rules and facts.
    - A response should be a numerical value indicating your confidence level between -100 (completely false) and 100 (completely true).

## Explanation of the Code

### Key Predicates

- **`solve(Goal, CF)`**
    - Starts the expert system, initializing known facts and solving for the given `Goal` with a resulting certainty factor `CF`.

- **`askuser(Goal, CF, Rules)`**
    - Asks the user about a particular goal and updates the known facts based on the user's response.

- **`build_proof(Goal, CF, Proof)`**
    - Constructs a proof tree for a given goal, showing how the certainty factor was derived.

- **`rule((Goal :- Premise), CF)`**
    - Defines a rule in the knowledge base with a certainty factor `CF`.

- **`askable(Goal)`**
    - Defines the askable goals, which the system can query the user about.

### Diagnostic Rules

- **Rules define how different diseases are diagnosed based on observed symptoms and examination results.**
    - Each rule has a certainty factor indicating the confidence in that rule.

### Emergency and Non-Emergency Diseases

- **The system differentiates between emergency and non-emergency conditions.**
    - Emergency conditions require immediate attention and have specific symptoms and examination results.
    - Non-emergency conditions are less urgent but still require proper diagnosis and treatment.

### Example Rules

- **Emergency Oral Cancer**
    ```prolog
    rule((disease(emergency_oral_cancer):-(is_emergency, examine_teeth(loose), examine_patient(lump_in_neck), examine_mouth(swollen_or_sore_lip))), 40).
    ```

- **Non-Emergency Oral Cancer**
    ```prolog
    rule((disease(nonemergency_oral_cancer):-(not(is_emergency), examine_teeth(loose), examine_patient(lump_in_neck), examine_mouth(swollen_or_sore_lip))), 40).
    ```

- **Caries**
    ```prolog
    rule((disease(caries):-(examine_mouth(bad_breath), examine_teeth(dark_spots), examine_teeth(sensitive), examine_teeth(has_pits), examine_teeth(poor_oral_hygiene))), 100).
    ```

- **Gingivitis**
    ```prolog
    rule((disease(gingivitis):-(symptom(inflamed_gums), examine_gums(bleeding))), 80).
    ```

- **Periodontitis**
    ```prolog
    rule((disease(periodontitis):-(disease(gingivitis), examine_teeth(gaps_present), examine_teeth(loose))), 80).
    ```

