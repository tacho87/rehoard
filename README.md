# REHOARD

## Introduction

Rehoard IS a project built in 2015 as an alternative to redux for internal use only. It is a simply sub/pub for react or vanilla js. It support local/session storage with redo/undo of actions. 




## Code Samples




export default class ReHoard {
    constructor() {
        this._reHoardPubSub = new ReHoardPubSub();
        window.StateHub = this;
    }

    /* Allow to change default settings. 
    settings = {
            persist : true,
            session : true,
            timeAlive : 1,
            undoRedo:  true,
            actionsHistory: true,
            actionsHistoryLimit:  100,
            typeMutable: false,
            production:  true
       };
   */
    changeSettings(settings) {
        this._reHoardPubSub.changeSettings(settings);
    }

    // Allows to create the state in a more explict way, a value must be passed to determine its type.
    // Dispatch will handle creation, so this is not needed.
    create(stateName, stateValue) {
        return this._reHoardPubSub._create(stateName, stateValue, "CREATION");
    }


    // dispatch changes, this will broadcast to any subscribers.
    // If state does not exists, it will create it, otherwise, it will update its value. 
    dispatch(stateName, stateValue, actionReference = "") {
        return this._reHoardPubSub.dispatch(stateName, stateValue, actionReference);
    }

    // subcribes to an existing state, if it does not exists it will throw an exception. 
    subscribe(stateName, listener) {
        return this._reHoardPubSub.subscribe(stateName, listener);
    }

    // will subscribe if the state exists, otherwise will queue it up once it is created. 
    subscribeWhenBecomesAlive(stateName, listener, unSubscribeCB) {
        return this._reHoardPubSub.subscribeWhenBecomesAlive(stateName, listener, unSubscribeCB);
    }

    // force a broadcast of the current value to everyone
    broadcastState(stateName) {
        return this._reHoardPubSub.broadcastState(stateName);
    }

    // returns current value of the state sync. No broadcasting happens
    getCurrentState(stateName) {
        return this._reHoardPubSub.getCurrentValue(stateName);
    }

    // Delete the current state and its listeners.
    deleteState(stateName) {
        return this._reHoardPubSub.deleteState(stateName);
    }

    // Redo the value state + action 
    redo(stateName) {
        return this._reHoardPubSub.redo(stateName);
    }

    // Undo the value to previous one
    undo(stateName) {
        return this._reHoardPubSub.undo(stateName);
    }
}




## Installation

npm install rehoard --save



