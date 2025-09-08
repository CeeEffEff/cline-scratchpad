# WORKFLOW Continuation Task

You must resume the workflow the previously active workflow ths currently in progress, picking up where it was left off.

active workflow relative path: [Add the name of the workflow here if you can remember it, otherwise suggest the memory bank be used]
You must continue with the workflow  GitHub PR Review Process - Detailed Sequence of Steps

## Completed Steps

[List of all the steps that have been completed with summary of outcome for each - if you have this knowledge]

## Current State

 [Describe your current state of processing files that were in the GitHub PR diff, and had just read]
    - Extracted code blocks include functions (`get_user_prompt_params`, `config_to_model`) and classes (`RestrictedBaseModel`, JsonBaseModel`,`QuestionAndAnswerResponse`)
    -`memory_bank/regex_refactor.md` and `memory_bank/activeContext.md` are updated with current status and next steps
    - `memory_bank/progress.md` is updated with the completion of the regex extraction and the next steps in organizing the code blocks

## Next Steps

1. Organize the extracted code blocks into a structured format for further processing
2. Generate documentation for the extracted code blocks
3. Implement additional refactoring tasks based on the structured format
4. Continue with the refactoring of `src/evaltask_model_migration.py` into multiple files

## Reference Information

- `src/evaltask_model_migration.py`: Contains functions (`get_user_prompt_params`, `config_to_model`) and classes that need to be solated. Example code blocks:

    ```python
    def get_user_prompt_params(line: str):
    try:
        params = json.loads(line)
        media_path = params.get("media_path", "")
        if not media_path:
        return None
        ext = media_path.split(".")[-1]
        if ext in ["jpg", "mp4"]:
        return params
    except Exception as e:
        print(e)
    return None
    ```

    ```python
    def config_to_model(model_name: str, eval_config: dict):
        _eval_gen_config:dict = eval_config["generate_content_config"]
        eval_gen_config = _eval_gen_config.copy()
        system_prompt = eval_gen_config.pop("system_instruction")
        eval_gen_config["response_schema"] = eval_gen_config.pop("response_json_schema")
        return GenerativeModel(
            model_name=model_name,
            safety_settings=SAFETY_SETTINGS,
            system_instruction=system_prompt,
            generation_config=GenerationConfig(
                **eval_gen_config
            )
        )
    ```
