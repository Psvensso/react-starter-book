# Loading external data

React does not know about the concept of data fetching. The React library helps you to build ui component that renders data based on props and state. The patterns we will now look at are based on experience and recommendations from either the React team or the community.

##### 

When doing async actions with React you want to make sure that the component that triggered the change are still there in the DOM take care of the promise \(or whatever your async callback pattern may be\). Therefore it's a good practise to handle async actions as high up in the component tree as possible. Somewhere "stable" that does not change, or a better option to make async actions even based.

##### Inline data fetching 

Although not a good idea this method is still in use. The basic indea is that you use setState in your async callback. Again, this is not a recommended practise but way work in simple scenarios.

###### PlayAlong@[006-Async](https://github.com/Psvensso/react-starter/blob/example-components/Scripts/Examples/Components/006-async.tsx)

    import * as React from "react";
    import { render } from "react-dom";

    interface IRedditListProps{
        subreddit: string;
    }

    interface IRedditListState{
        reddits: IRedditPost[]
    }

    interface IRedditPost{
        kind: string;
        data: {
            subreddit: string,
            selftext_html: string,
            selftext: string;
            id: string;
            score: number;
            downs: number;
            url: string;
            title: string;
            created_utc: number;
        }
    }

    export class RedditList extends React.Component<IRedditListProps,IRedditListState>{
        constructor(){
            super();
            this.state={
                reddits: []
            }
        }
        componentDidMount(){
            fetch(`https://www.reddit.com/r/${this.props.subreddit}.json`).then(r => r.json()).then((resp:any) => {
                this.setState({
                    reddits: resp.data.children
                });
            });
        }
        render(){

            return <div className="container" style={{marginTop: 50}}>
                <div className="list-group">
                {this.state.reddits.map((reddit, i) => (
                    <a href={reddit.data.url} target="_blank" className="list-group-item" key={i}>
                        {reddit.data.score} - {reddit.data.title}
                    </a>
                ))}
            </div>
            </div>
        }
    }

    render(
        <div style={{ clear: "both" }}>
            <p>006-Async.tsx</p>
            <RedditList subreddit="reactjs"/>
        </div>,
        document.getElementById("asyncex") 
    );

The other, much more robust way is with a state management API. We will use the well adopted [Redux ](https://github.com/reactjs/redux)library.

