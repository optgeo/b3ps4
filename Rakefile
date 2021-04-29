require 'yaml'
require 'json'

YAML_PATH = 'config.yml'
JS_PATH = 'docs/config.js'

TOKEN = 'pk.eyJ1IjoiaGZ1IiwiYSI6ImlRSGJVUTAifQ.rTx380smyvPc1gUfZv1cmw'
ALIGNMENT = 'right'
ROTATE = true

def process(config)
  config[:accessToken] = TOKEN
  config[:theme] = 'light'
  config[:showMarkers] = false
  n = 0
  config['chapters'].each {|chapter|
    n += 1
    chapter[:id] = "chapter-#{n}"
    chapter[:alignment] = ALIGNMENT
    chapter[:callback] = nil
    chapter[:hidden] = false
    chapter[:mapAnimation] = 'flyTo'
    chapter[:rotateAnimation] = ROTATE
    chapter[:onChapterEnter] = []
    chapter[:onChapterExit] = []
    r = chapter['hash'].split('/').map{|v| v.to_f}
    chapter[:location] = {
      :zoom => r[0],
      :center => [
        r[2],
        r[1]
      ],
      :bearing => r[3],
      :pitch => r[4]
    }
  }
  JSON.pretty_generate(config)
end

desc 'create config.js'
task :config do
  w = File.open(JS_PATH, 'w')
  w.print [
    'const config = ',
    process(YAML.load(File.read(YAML_PATH)))
  ].join(), "\n"
  w.close
end
