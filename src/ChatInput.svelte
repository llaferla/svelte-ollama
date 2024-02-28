<script lang="ts">
    import { entries } from "./store";
    import ChatEntryModel from "./ChatEntryModel";
    import axios from "axios";
    import type { AxiosResponse } from "axios";

    let value: string;
    async function send() {
        console.log("Sending..." + value);
        let model = new ChatEntryModel();
        model.prompt = value;
        model.response = "Waiting...";
        entries.set([...$entries, model]);
        
        let answer = await fetchData({ "model": "llama2", "prompt": model.prompt });
        model.response = answer;
        console.log(model.response);

        entries.set([...$entries]);
        value = "";
    }

    async function fetchData(data: object): Promise<string> {
        let answer: string = "";
        try {
            answer = "";
            const url = "http://localhost:11434/api/generate";

            const response: AxiosResponse<any, any> = await axios.post(
                url,
                data,
            );

            const json: string = response.data as string;
            const lines: string[] = json.split(/\r?\n/);

            for (const line of lines) {
                if (line.trim() !== "") {
                    const parsedline = JSON.parse(line);
                    if (parsedline.done == false) {
                        answer += parsedline.response;
                    }
                }
            }
            console.log("Answer:", answer); // Log final answer
        } catch (error) {
            console.error("Error fetching data:", error);
        }

        return answer;
    }
</script>

<div>
    <input type="text" bind:value />
    <button on:click={send}>Send</button>
</div>
