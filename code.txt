var botScriptExecutor = require('bot-script').executor;
var scr_config = require('./scr_config.json');

function MessageHandler(context, event) {
   	if(event.message == 'startchattingevent'){
   		context.sendResponse("Hello welcome to the chat. You can now ask your question.");
   	}else if (event.message == "How does solar energy work?"){
   		context.sendResponse("When the sun shines onto a solar panel, energy from sunlight is absorbed by the PV cells in the panel. This energy creates electrical charges that is converted into power for your home. ");
   	}else if (event.message == "How much electricity can a solar panel produce?"){
   		context.sendResponse("Most residential solar panels on today's market are rated to produce between 400 watts to 1 kW each per hour. Domestic solar panel systems typically have a capacity of between 3 kW and 12 kW.");
   	}else if (event.message == "How much does a solar panel cost?"){
   		context.sendResponse("The average cost for solar panels is $3–$5 per watt, totaling $15,000–$20,000 for a typical 5 kilowatt (kW) system.");
   	}else if (event.message == "How does solar energy impact electricity costs?"){
   		context.sendResponse("With solar energy, you can lower your electricity cost by as much as 50% to 100%.");
   	}else if (event.message == "Is solar energy reliable?"){
   		context.sendResponse("Solar energy is a more reliable energy source than fossil fuels because it is renewable. ");
   	}else if (event.message == "What is your company name?"){
   		context.sendResponse("We are Greep Technologies, Inc.");
   	}else if (event.message == "Where is your company based?"){
   		context.sendResponse("Our company is based in Singapore with sattelite offices in the Philippines.");
   	}else if (event.message == "When is your company established?"){
   		context.sendResponse("Greep Technologies was established in 2022.");
   	}else if (event.message == "What is your company purpose?"){
   		context.sendResponse("Our purpose is to connect eco-warriors and to build a greener world.");
   	}else if (event.message == "What is your company mission?"){
   		context.sendResponse("Our mission is to empower the world to a greener future.");
   	}else if (event.message == "What are the requirements for installing solar panels for my home?"){
   		context.sendResponse("If you are interested in acquiring solar panels for your home, kindly click here.");
   	}else if (event.message == "What is the ideal solar power system setup for my home?"){
   		context.sendResponse("Monocrystalline solar panels are the most ideal and efficient option often used for larger energy systems in commercial and residential properties. Monocrystalline panel sized vary which make them suitable for smaller installations. Click here to know more.");
   	}else if (event.message == "How many solar panels do I need to power my home?"){
   		context.sendResponse("The number of solar panels depends on the power consumption of your home. Would like to me to help you assess your solar power requirements? (Yes or No)");
   	}else if (event.message == "How much can I save when I use solar energy for my home?"){
   		context.sendResponse("With solar energy, you can lower your electricity cost by as much as 50% to 100%.");
   	}else if (event.message == "How do I finance my solar power system?"){
   		context.sendResponse("Greep is community of eco-warriors with passionate investors who can help finance your solar project. To find out more, click here.");
   	}else if (event.message == "How can I invest in solar power projects?"){
   		context.sendResponse("Greep is a community of eco-warrios who believe in solar energy and are willing to solarize their homes. You can find a suitable solar project to invest through our platform.");
   	}else if (event.message == "How much money do I need to invest?"){
   		context.sendResponse("The minimum investment is only $100.");
   	}else if (event.message == "What is the return on investment?"){
   		context.sendResponse("With Greep, the average return on investment is between 10 to 15%");
   	}else if (event.message == "When is the total investment due?"){
   		context.sendResponse("");
   	}else if (event.message == "Can you further explain how it works?"){
   		context.sendResponse("");
   	}
   	
}

function EventHandler(context, event) {
    context.simpledb.roomleveldata = {};
    MessageHandler(context, event);
}


function ScriptHandler(context, event){
    var options = Object.assign({}, scr_config);
    options.current_dir = __dirname;
    //options.default_message = "Sorry Some Error Occurred.";
    // You can add any start point by just mentioning the <script_file_name>.<section_name>
    // options.start_section = "default.main";
    options.success = function(opm){
        context.sendResponse(JSON.stringify(opm));
    };
    options.error = function(err) {
        console.log(err.stack);
        context.sendResponse(options.default_message);
    };
    botScriptExecutor.execute(options, event, context);
}

function HttpResponseHandler(context, event) {
    if (event.geturl === "http://ip-api.com/json")
        context.sendResponse('This is response from http \n' + JSON.stringify(event.getresp, null, '\t'));
}

function DbGetHandler(context, event) {
    context.sendResponse("testdbput keyword was last sent by:" + JSON.stringify(event.dbval));
}

function DbPutHandler(context, event) {
    context.sendResponse("testdbput keyword was last sent by:" + JSON.stringify(event.dbval));
}

function HttpEndpointHandler(context, event) {
    context.sendResponse('This is response from http \n' + JSON.stringify(event, null, '\t'));
}

function LocationHandler(context, event) {
    context.sendResponse("Got location");
};

exports.onMessage = MessageHandler;
exports.onEvent = EventHandler;
exports.onHttpResponse = HttpResponseHandler;
exports.onDbGet = DbGetHandler;
exports.onDbPut = DbPutHandler;
if (typeof LocationHandler == 'function') { exports.onLocation = LocationHandler; }
if (typeof HttpEndpointHandler == 'function') { exports.onHttpEndpoint = HttpEndpointHandler; }
