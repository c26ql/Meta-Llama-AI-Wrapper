import requests

class MetaAI:
    def __init__(self, api_key, base_url='https://api.metaai.com/v1'):
        self.api_key = api_key
        self.base_url = base_url
        self.headers = {
            'Authorization': f'Bearer {self.api_key}',
            'Content-Type': 'application/json'
        }

    def _get(self, endpoint, params=None):
        url = f'{self.base_url}/{endpoint}'
        response = requests.get(url, headers=self.headers, params=params)
        return self._handle_response(response)

    def _post(self, endpoint, data=None):
        url = f'{self.base_url}/{endpoint}'
        response = requests.post(url, headers=self.headers, json=data)
        return self._handle_response(response)

    def _handle_response(self, response):
        if response.status_code != 200:
            raise Exception(f'API request failed with status {response.status_code}: {response.text}')
        return response.json()

    def get_model_info(self, model_id):
        endpoint = f'models/{model_id}'
        return self._get(endpoint)

    def generate_text(self, model_id, prompt, max_tokens=50, temperature=1.0):
        endpoint = f'models/{model_id}/generate'
        data = {
            'prompt': prompt,
            'max_tokens': max_tokens,
            'temperature': temperature
        }
        return self._post(endpoint, data)

    def list_models(self):
        endpoint = 'models'
        return self._get(endpoint)

# Example usage:
if __name__ == '__main__':
    api_key = 'your_meta_ai_api_key_here'
    meta_ai = MetaAI(api_key)

    # List available models
    models = meta_ai.list_models()
    print(models)

    # Get information about a specific model
    model_id = 'example_model_id'
    model_info = meta_ai.get_model_info(model_id)
    print(model_info)

    # Generate text using a specific model
    prompt = 'Once upon a time'
    generated_text = meta_ai.generate_text(model_id, prompt)
    print(generated_text)
