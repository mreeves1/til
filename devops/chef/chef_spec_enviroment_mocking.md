# ChefSpec environment mocking

Based on http://stackoverflow.com/questions/21382833/how-can-i-use-chefspec-during-refactoring-of-environments-roles-nodes

Sometimes you want cookbook recipe behavior to vary depending on the enviroment. Here is a snippet to do that:

```
  it 'creates robots.txt in shared for prod environments' do
    # We need to mock that we are the prod env
    prod_env_file = File.open('../../environments/production.json', "rb")
    env_attr = JSON.parse(prod_env_file.read)
    env = Chef::Environment.json_create(env_attr)
    chef_run.node.stub(:chef_environment).and_return('production')
    Chef::Environment.stub(:load).and_return(env)

    chef_run.converge('kabam::default', described_recipe)
    expect(chef_run).to render_file('/var/www/com2/shared/robots.txt').with_content(/Disallow: \/assets\/\*$/) # Disallow: /assets/*
  end
```
